.. index::
   single: Forms; Fields; collection

Type de champ Collection
========================

Ce type de champ est utilis� pour rendre une � collection � de champs ou de formulaires.
Plus simplement, ce pourrait �tre un tableau de champs ``text`` qui remplirait un tableau
de champs``emails``. 
Dans les cas les plus complexes, vous pourrez imbriquer des formulaires entiers, ce qui
est tr�s utile lorsque vous cr�erez des formulaires avec des relations one-to-many
(par exemple un produit pour lequel vous pouvez g�rer plusieurs photos de ce produit).

+-------------+-----------------------------------------------------------------------------+
| Rendu comme | d�pend de l'option `type`_                                                  |
+-------------+-----------------------------------------------------------------------------+
| Options     | - `type`_                                                                   |
|             | - `options`_                                                                |
|             | - `allow_add`_                                                              |
|             | - `allow_delete`_                                                           |
|             | - `prototype`_                                                              |
+-------------+-----------------------------------------------------------------------------+
| Options     | - `label`_                                                                  |
| h�rit�es    | - `error_bubbling`_                                                         |
|             | - `by_reference`_                                                           |
+-------------+-----------------------------------------------------------------------------+
| Type Parent | :doc:`form</reference/forms/types/form>`                                    |
+-------------+-----------------------------------------------------------------------------+
| Classe      | :class:`Symfony\\Component\\Form\\Extension\\Core\\Type\\CollectionType`    |
+-------------+-----------------------------------------------------------------------------+

Utilisation basique
-------------------

Ce type est utilis� quand vous voulez g�rer une collection d'items similaires dans 
un formulaire. Par exemple, supposez que vous avez un champ ``emails`` qui correspond
� un tableau d'adresses email. Dans le formulaire, vous voudrez afficher chaque adresse
email dans son propre champ input::

    $builder->add('emails', 'collection', array(
        // chaque item du tableau sera un champ � email �
        'type'   => 'email',
        // ces options sont pass�es � chaque type � email �
        'options'  => array(
            'required'  => false,
            'attr'      => array('class' => 'email-box')
        ),
    ));

La fa�on la plus simple de rendre ces champs est de tout faire en un coup :

.. configuration-block::

    .. code-block:: jinja
    
        {{ form_row(form.emails) }}

    .. code-block:: php
    
        <?php echo $view['form']->row($form['emails]) ?>

Une m�thode plus flexible pourrait ressembler � ceci :

.. configuration-block::

    .. code-block:: html+jinja
    
        {{ form_label(form.emails) }}
        {{ form_errors(form.emails) }}

        <ul>
        {% for emailField in form.emails %}
            <li>
                {{ form_errors(emailField) }}
                {{ form_widget(emailField) }}
            </li>
        {% endfor %}
        </ul>

    .. code-block:: html+php

        <?php echo $view['form']->label($form['emails']) ?>
        <?php echo $view['form']->errors($form['emails']) ?>
        
        <ul>
        {% for emailField in form.emails %}
        <?php foreach ($form['emails'] as $emailField): ?>
            <li>
                <?php echo $view['form']->errors($emailField) ?>
                <?php echo $view['form']->widget($emailField) ?>
            </li>
        <?php endforeach; ?>
        </ul>

Dans les deux cas, aucun champ input ne sera affich� tant que le tableau ``emails``
ne contient aucune adresse email.

Dans cet exemple simple, il est toujours impossible d'ajouter de nouvelles adresses
ou d'en supprimer. Ajouter une nouvelle adresse est possible en utilisant l'option
`allow_add`_ (et optionnellement l'option `prototype`_) (voir l'exemple ci-dessous). 
Supprimer des emails du tableau ``emails`` est possible gr�ce � l'option `allow_delete`_.

Ajouter et supprimer des items
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Si `allow_add`_ est d�fini � ``true``, alors tout item non reconnu qui est envoy�
sera ajout� dans le tableau de fa�on transparente. C'est g�nial en th�orie, mais en
pratique, il vous faudra plus d'efforts pour adapter la partie client JavaScript.

En poursuivant avec l'exemple pr�c�dent, supposez que vous commencez avec deux emails
dans votre tableau de donn�es ``emails``.  Dans ce cas, deux champs input seront rendus,
ce qui ressemblera � quelque chose comme ceci (�a d�pendra du nom de votre formulaire) :

.. code-block:: html

    <input type="email" id="form_emails_1" name="form[emails][0]" value="foo@foo.com" />
    <input type="email" id="form_emails_1" name="form[emails][1]" value="bar@bar.com" />

Pour autoriser votre utilisateur � ajouter un autre email, d�finissez juste `allow_add`_
� ``true`` et, en JavaScript, rendez un autre champ avec le nom ``form[emails][2]``
(en incr�mentant � chaque nouveau champ).

Pour vous aider � faire cela plus facilement, d�finir l'option `prototype`_ � ``true`` 
permet de rendre un � template � de champ que vous pourrez utiliser dans votre fichier
JavaScript afin de cr�er dynamiquement des nouveaux champs. Un champ prototype rendu
ressemblera � :

.. code-block:: html

    <input type="email" id="form_emails___name__" name="form[emails][__name__]" value="" />

En rempla�ant ``__name__`` par une valeur unique (ex: ``2``), vous pouvez construire
et ins�rer des nouveaux champs HTML dans votre formulaire.

Si vous utilisez jQuery, un exemple simple pourrait ressembler � ceci. Si vous rendez
votre collection de champs en une seule fois (ex: ``form_row(form.emails)``), alors
les choses sont encore plus simples puisque l'attribut ``data-prototype`` est automatiquement
rendu pour vous (avec une leg�re diff�rence - voir la note ci-dessous) et vous n'avez
besoin que du JavaScript :

.. configuration-block::

    .. code-block:: html+jinja
    
        <form action="..." method="POST" {{ form_enctype(form) }}>
            {# ... #}

            {# stocke le prototype dasn l'attribut data-prototype #}
            <ul id="email-fields-list" data-prototype="{{ form_widget(form.emails.get('prototype')) | e }}">
            {% for emailField in form.emails %}
                <li>
                    {{ form_errors(emailField) }}
                    {{ form_widget(emailField) }}
                </li>
            {% endfor %}
            </ul>
        
            <a href="#" id="add-another-email">Add another email</a>
        
            {# ... #}
        </form>

        <script type="text/javascript">
            // garde une trace du nombre de champs email qui ont �t� affich�s
            var emailCount = '{{ form.emails | length }}';

            jQuery(document).ready(function() {
                jQuery('#add-another-email').click(function() {
                    var emailList = jQuery('#email-fields-list');

                    // parcourt le template prototype
                    var newWidget = emailList.attr('data-prototype');
                    // remplace les "__name__" utilis�s dans l'id et le nom du prototype
                    // par un nombre unique pour chaque email
                    // le nom de l'attribut final ressemblera � name="contact[emails][2]"
                    newWidget = newWidget.replace(/__name__/g, emailCount);
                    emailCount++;

                    // cr�er une nouvelle liste d'�l�ments et l'ajoute � notre liste
                    var newLi = jQuery('<li></li>').html(newWidget);
                    newLi.appendTo(jQuery('#email-fields-list'));

                    return false;
                });
            })
        </script>

.. tip::

    Si vous rendez une collection enti�re en une seule fois, alors le prototype
	est automatiquement disponible dans l'attribut ``data-prototype`` de l'�l�ment
    (ex: ``div`` ou ``table``) qui encadre votre collection. La seule diff�rence
	c'est que le � form row � est rendu pour vous en entier, ce qui signifie que vous
	n'aurez pas � l'encadrer dans un conteneur quelconque comme nous l'avions fait
	ci-dessus.

Options du champ
----------------

type
~~~~

**type**: ``string`` ou :class:`Symfony\\Component\\Form\\FormTypeInterface` **required**

C'est le type de champ pour chaque item dans la collection (ex: ``text``, ``choice``,
etc). Par exemple, si vous avez un tableau d'adresses email, vous utiliserez le type 
:doc:`email</reference/forms/types/email>`. Si vous voulez imbriquer une collection
d'un autre formulaire, cr�ez une nouvelle instance de votre type de formulaire et passez
la dans cette option.

options
~~~~~~~

**type**: ``array`` **default**: ``array()``

C'est le tableau qui est pass� au type formulaire sp�cifi� dans l'option `type`_.
Par exemple, si vous utilisez le type :doc:`choice</reference/forms/types/choice>`
dans l'option `type`_ (pa exemple pour une collection de menus d�roulants), alors
vous devrez au moins passer l'option ``choices`` au type sous-jacent::

    $builder->add('favorite_cities', 'collection', array(
        'type'   => 'choice',
        'options'  => array(
            'choices'  => array(
                'nashville' => 'Nashville',
                'paris'     => 'Paris',
                'berlin'    => 'Berlin',
                'london'    => 'London',
            ),
        ),
    ));

allow_add
~~~~~~~~~

**type**: ``Boolean`` **default**: ``false``

Si cette option est d�finie � ``true``, alors tout item non reconnu qui est soumis
sera ajout� � la collection comme nouvel item. Le tableau final contiendra les items
existants ainsi que les nouveaux items qui auront �t� soumis. Regardez l'exemple
ci-dessus pour plus de d�tails.

L'option `prototype`_ peut �tre utilis�e pour rendre un prototype d'item qui pourra �tre
utilis� - en JavaScript - pour cr�er des nouveaux items de formulaire dynamiquement
c�t� client. Pour plus d'informations, voyez l'exemple ci-dessus et :ref:`cookbook-form-collections-new-prototype`.

.. caution::
    Si vous imbriquez des autres formulaires entiers pour prendre en compte une
	relation one-to-many en base de donn�es, vous devrez vous assurer manuellement
	que la cl� �trang�re de ces nouveaux objets est correctement d�finie. Si vous
	utilisez Doctrine, ce ne sera pas fait automatiquement. Voyez le lien ci-dessus
	pour plus de d�tails.

allow_delete
~~~~~~~~~~~~

**type**: ``Boolean`` **default**: ``false``

Si cette option est d�finie � ``true``, alors si un item existant ne se retrouve
pas dans les donn�es soumises, il sera supprim� du tableau d'items final. Cela signifie
que vous pouvez impl�menter un bouton � Supprimer � en JavaScript qui supprimera
simplement un �l�ment formulaire du DOM. Quand l'utilisateur soumettra le formulaire,
l'absence de cet �l�ment des donn�es soumises entrainera la suppression de l'item
dans le tableau final.

Pour plus d'informations, lisez :ref:`cookbook-form-collections-remove`.

.. caution::
    
	Soyez prudents lorsque vous utilisez cette option en imbriquant une collection
	d'objets. Dans ce cas, si un formulaire imbriqu� est supprim�, il *sera* bien
	retir� du tableau final d'objets. Pourtant, selon la logique de votre application,
	lorsque l'un de ces objets est supprim�, vous voudrez probablement supprimer,
	ou au moins retirer, les cl� �trang�res qui lient cet objet � l'objet principal.
	Rien de tout cela n'est fait automatiquement. Pour plus d'informations, lisez
    :ref:`cookbook-form-collections-remove`.

prototype
~~~~~~~~~

**type**: ``Boolean`` **default**: ``true``

Cette option est utile lorsqu'elle est associ�e � l'option `allow_add`_. Si elle
est � ``true`` (et que `allow_add`_ est aussi � ``true``), un attribut sp�cial � prototype �
sera disponible pour que vous puissiez rendre un exemple de � template � � votre page
afin de sp�cifier ce � quoi le nouvel �lement doit ressembler. L'attribut ``name``
donn� � cet �l�ment est ``__name__``. Cela vous permet d'ajouter un bouton � Ajouter un
�l�ment � en JavaScript qui parcourt le prototype, remplace ``__name__`` par un
nom unique ou un num�ro, et le rend � votre formulaire. Lors de la soumission, il sera
ajout� � votre tableau de donn�es gr�ce � l'option `allow_add`_.

Le champ prototype peut �tre rendu via la variable ``prototype`` du champ collection :

.. configuration-block::

    .. code-block:: jinja
    
        {{ form_row(form.emails.get('prototype')) }}

    .. code-block:: php
    
        <?php echo $view['form']->row($form['emails']->get('prototype')) ?>

Notez que tout ce dont vous avez vraiment besoin c'est le � widget �, mais selon la
mani�re dont vous rendez votre formulaire, utiliser le � form row � peut �tre plus
facile pour vous.

.. tip::
    
	Si vous rendez une enti�re collection de champs en une seule fois, alors le
	prototype du � form row � est automatiquement disponible dans l'attribut ``data-prototype``
	de l'�l�ment (ex ``div`` ou ``table``) qui encadre votre collection.

Pour plus de d�tails sur l'utilisation de cette option, lisez l'exemple ci-dessus
ou :ref:`cookbook-form-collections-new-prototype`.

Options h�rit�es
----------------

Ces options sont h�rit�es du type :doc:`field</reference/forms/types/form>`.
Toutes les options ne sont pas list�es ici, seulement celles qui s'appliquent le plus
� ce type :

.. include:: /reference/forms/types/options/label.rst.inc

error_bubbling
~~~~~~~~~~~~~~

**type**: ``Boolean`` **default**: ``true``

.. include:: /reference/forms/types/options/_error_bubbling_body.rst.inc

.. include:: /reference/forms/types/options/by_reference.rst.inc