.. index::
   single: Forms; Fields; choice

Type de champ Entity
====================

Un champ ``choice`` sp�cial qui est con�u pour charger ses options d'une entit�
Doctrine. Par exemple, si vous avez une entit� ``Category``, vous pourrez utiliser
ce champ pour afficher une liste ``select`` de tout ou de certains objets ``Category``
depuis la base de donn�es.

+-------------+----------------------------------------------------------------------+
| Rendu comme | peut �tre plusieurs balises (voir :ref:`forms-reference-choice-tags`)|
+-------------+----------------------------------------------------------------------+
| Options     | - `class`_                                                           |
|             | - `property`_                                                        |
|             | - `query_builder`_                                                   |
|             | - `em`_                                                              |
+-------------+----------------------------------------------------------------------+
| Options     | - `required`_                                                        |
| h�rit�es    | - `label`_                                                           |
|             | - `multiple`_                                                        |
|             | - `expanded`_                                                        |
|             | - `preferred_choices`_                                               |
|             | - `empty_value`_                                                     |
|             | - `read_only`_                                                       |
|             | - `error_bubbling`_                                                  |
+-------------+----------------------------------------------------------------------+
| Type parent | :doc:`choice</reference/forms/types/choice>`                         |
+-------------+----------------------------------------------------------------------+
| Classe      | :class:`Symfony\\Bridge\\Doctrine\\Form\\Type\\EntityType`           |
+-------------+----------------------------------------------------------------------+

Utilisation de base
-------------------

Le type ``entity`` n'a qu'une seule option obligatoire : l'entit� qui doit �tre list�e
dans le champ Choice::

    $builder->add('users', 'entity', array(
        'class' => 'AcmeHelloBundle:User',
    ));

Dans ce cas, tout les objets ``User`` seront charg�s depuis la base de donn�es et seront
affich�s soit comme une balise ``select``, soit un ensemble de boutons radio ou de checkboxes
(cela d�pendra des valeurs des options ``multiple`` et ``expanded``).

Utiliser une requ�te personnalis�e pour les entit�s
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Si vous avez besoin de sp�cifier une requ�te personnalis�e � utiliser pour charger
les entit�es (par exemple si vous ne voulez que certaines entit�s, ou que vous voulez
les classer), utilisez l'option ``query_builder``. La fa�on la plus simple d'utiliser
cette option est la suivante::

    use Doctrine\ORM\EntityRepository;
    // ...

    $builder->add('users', 'entity', array(
        'class' => 'AcmeHelloBundle:User',
        'query_builder' => function(EntityRepository $er) {
            return $er->createQueryBuilder('u')
                ->orderBy('u.username', 'ASC');
        },
    ));

.. include:: /reference/forms/types/options/select_how_rendered.rst.inc

Options du champ
----------------

class
~~~~~

**type**: ``string`` **obligatoire*

La classe de votre entit� (ex: ``AcmeStoreBundle:Category``). Cela peut �tre
le nom complet de la classe (ex: ``Acme\StoreBundle\Entity\Category``) ou son alias
(voir ci-dessus).

property
~~~~~~~~

**type**: ``string``

C'est la propri�t� qui doit �tre utilis�e pour afficher l'entit� sous forme de
texte dans l'�l�ment HTML. Si vous le laissez vite, l'objet entit� sera converti
en texte et devra alors impl�menter la m�thode ``__toString()``.

query_builder
~~~~~~~~~~~~~

**type**: ``Doctrine\ORM\QueryBuilder`` or a Closure

Si elle est sp�cifi�e, cette option sera utilis�e pour requ�ter un sous-ensemble
d'objets (et leur classement) qui sera affich� dans le champ. La valeur de cette
option peut �tre soit un objet ``QueryBuilder`` soit une Closure. Si vous utilisez
une Closure, elle ne doit prendre qu'un seul argument qui est l'objet ``EntityRepository``
de l'entit�.

em
~~

**type**: ``string`` **default**: le gestionnaire d'entit� par d�faut

Si elle est sp�cifi�e, cette option d�finit le gestionnaire d'entit� (entity manager)
qui sera utilis� pour charger les objets au lieu du gestionnaire par d�faut.

Options h�rit�es
----------------

Ces options sont h�rit�es du type :doc:`choice</reference/forms/types/choice>` :

.. include:: /reference/forms/types/options/multiple.rst.inc

.. include:: /reference/forms/types/options/expanded.rst.inc

.. include:: /reference/forms/types/options/preferred_choices.rst.inc

.. include:: /reference/forms/types/options/empty_value.rst.inc

Ces options sont h�rit�es du type :doc:`field</reference/forms/types/field>` :

.. include:: /reference/forms/types/options/required.rst.inc

.. include:: /reference/forms/types/options/label.rst.inc

.. include:: /reference/forms/types/options/read_only.rst.inc

.. include:: /reference/forms/types/options/error_bubbling.rst.inc
