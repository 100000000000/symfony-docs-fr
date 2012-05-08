.. index::
   single: Assetic; Introduction

Comment utiliser Assetic pour g�rer vos ressources
==================================================

Assetic associe deux concepts majeurs : les ressources et les filtres. Les ressources
sont des fichiers comme les feuilles de style, les JavaScript et les images. Les
filtres peuvent �tre appliqu�s � ces fichiers avant qu'ils soient servis au
navigateur. Cela permet de g�rer s�paremment les fichiers ressources qui sont stock�s
par l'application des fichiers qui sont r�ellement pr�sent�s � l'utilisateur.

Sans Assetic, vous servez directement les fichiers qui sont stock�s dans votre
application :

.. configuration-block::

    .. code-block:: html+jinja

        <script src="{{ asset('js/script.js') }}" type="text/javascript" />

    .. code-block:: php

        <script src="<?php echo $view['assets']->getUrl('js/script.js') ?>"
                type="text/javascript" />

Mais *avec* Assetic, vous pouvez manipuler ces ressources de la mani�re dont
vous le d�sirez (ou les charger o� vous le voulez) avant de les	servir. Cela
signifie que vous pouvez :

* Minifier et combiner toutes vos CSS ou vos fichiers JavaScript

* Ex�cuter tous (ou juste une partie) vos fichiers CSS ou JS en passant par des
  compilateurs comme LESS, SASS ou CoffeeScript.

* Optimiser vos images

Ressources
----------

Utiliser Assetic plut�t que servir les fichiers directement offre de nombreux avantages.
Les fichiers n'ont pas besoin d'�tre stock�s l� o� il seront servis, et peuvent
provenir de plusieurs sources, notamment d'un bundle :

.. configuration-block::

    .. code-block:: html+jinja

        {% javascripts
            '@AcmeFooBundle/Resources/public/js/*'
        %}
        <script type="text/javascript" src="{{ asset_url }}"></script>
        {% endjavascripts %}

    .. code-block:: html+php

        <?php foreach ($view['assetic']->javascripts(
            array('@AcmeFooBundle/Resources/public/js/*')) as $url): ?>
        <script type="text/javascript" src="<?php echo $view->escape($url) ?>"></script>
        <?php endforeach; ?>

.. tip::

    Pour inclure une feuille de style, vous pouvez utiliser le m�me proc�d� que
	ci-dessus, sauf que vous utiliserez le tag `stylesheets` :

    .. configuration-block::

        .. code-block:: html+jinja

            {% stylesheets
                '@AcmeFooBundle/Resources/public/css/*'
            %}
            <link rel="stylesheet" href="{{ asset_url }}" />
            {% endstylesheets %}

        .. code-block:: html+php

            <?php foreach ($view['assetic']->stylesheets(
                array('@AcmeFooBundle/Resources/public/css/*')) as $url): ?>
            <link rel="stylesheet" href="<?php echo $view->escape($url) ?>" />
            <?php endforeach; ?>

Dans cet exemple, tous les fichiers du r�pertoire ``Resources/public/js/`` du bundle
``AcmeFooBundle`` seront charg�s et servis depuis un autre r�pertoire. La balise
r�ellement g�n�r�e pourrait ressembler � ceci :

.. code-block:: html

    <script src="/app_dev.php/js/abcd123.js"></script>

.. note::
    
	C'est un point essentiel : une fois que vous laissez Assetic g�rer vos ressources,
	les fichiers sont servis depuis diff�rents emplacements. Cela *peut* poser des
	probl�mes avec les CSS qui utilisent des images r�f�renc�es par des chemins
	relatifs. Pourtant, ce probl�me peut �tre r�solu en utilisant le filtre
	``cssrewrite`` qui met � jour les chemins dans les fichiers CSS pour prendre
    en compte leur nouvel emplacement.

Combiner des ressources
~~~~~~~~~~~~~~~~~~~~~~~

Vous pouvez aussi combiner plusieurs fichiers en un seul. Cela aide � r�duire le
nombre de requ�tes HTTP, ce qui est tr�s important pour les performances. Cela
vous permet aussi de maintenir les fichiers plus facilement en les d�coupants
en petites parties faciles � g�rer. Cela peut �tre un plus pour la r�usabilit�
de votre projet puisque vous pouvez facilement s�parer les fichiers sp�cifiques
au projet des fichiers qui peuvent �tre r�utilis�s dans d'autres applications,
mais toujours les servir comme un fichier unique :

.. configuration-block::

    .. code-block:: html+jinja

        {% javascripts
            '@AcmeFooBundle/Resources/public/js/*'
            '@AcmeBarBundle/Resources/public/js/form.js'
            '@AcmeBarBundle/Resources/public/js/calendar.js'
        %}
        <script src="{{ asset_url }}"></script>
        {% endjavascripts %}

    .. code-block:: html+php

        <?php foreach ($view['assetic']->javascripts(
            array('@AcmeFooBundle/Resources/public/js/*',
                  '@AcmeBarBundle/Resources/public/js/form.js',
                  '@AcmeBarBundle/Resources/public/js/calendar.js')) as $url): ?>
        <script src="<?php echo $view->escape($url) ?>"></script>
        <?php endforeach; ?>

En environnement de `dev`, chaque fichier est toujours servi individuellement
pour que vous puissiez d�bugguer plus facilement. Cependant, en environnement de
`prod`, ils seront affich�s dans une unique balise `script`.

.. tip::

    Si vous d�couvrez Assetic et essayez d'utiliser votre application en
    environnement de ``prod`` (en utilisant le contr�leur ``app.php``), vous
    verrez probablement que vos CSS et JS plantent. Pas de panique ! C'est
    fait expr�s. Pour plus de d�tails sur l'utilisation d'Assetic en
    environnement de `prod`, lisez :ref:`cookbook-assetic-dumping`.

Et combiner les fichiers ne s'applique pas uniquement � *vos* fichiers. Vous
pouvez aussi utiliser Assetic pour combiner les ressources tierces, comme jQuery,
� vos fichiers dans un fichier unique :

.. configuration-block::

    .. code-block:: html+jinja

        {% javascripts
            '@AcmeFooBundle/Resources/public/js/thirdparty/jquery.js'
            '@AcmeFooBundle/Resources/public/js/*'
        %}
        <script src="{{ asset_url }}"></script>
        {% endjavascripts %}

    .. code-block:: html+php

        <?php foreach ($view['assetic']->javascripts(
            array('@AcmeFooBundle/Resources/public/js/thirdparty/jquery.js',
                  '@AcmeFooBundle/Resources/public/js/*')) as $url): ?>
        <script src="<?php echo $view->escape($url) ?>"></script>
        <?php endforeach; ?>

Filtres
-------

Une fois qu'elles sont g�r�es par Assetic, vous pouvez appliquer des filtres
� vos ressources avant qu'elles soient servies. Cela inclut les filtres qui
compressent vos ressources pour r�duire la taille des fichiers (pour de
meilleures performances). D'autres filtres peuvent compiler des fichiers
CoffeeScript en JavaScript ou couvertir vos fichiers SASS en CSS.
En fait, Assetic poss�de une longue liste de filtres.

Plusieurs de ces filtres ne font pas le travail directement, mais utilisent
des librairies tierces pour faire le gros du travail. Cela signifie que vous
devrez souvent installer une librairie tierce pour utiliser un filtre. Le grand
avantage d'utiliser Assetic pour faire appel � ces librairies (plut�t que de les
utiliser directement) est qu'au lieu de les ex�cuter � la main apr�s avoir modifi�
les fichiers, Assetic prendra tout en charge pour vous, et supprimera d�finitivement
cette �tape du processus de d�veloppement et de d�ploiement.

Pour utiliser un filtre, vous aurez d'abord besoin de le sp�cifier dans la
configuration d'Assetic. Ajouter un filtre dans la configuration ne signifie
pas qu'il est utilis�, mais juste qu'il est pr�t � l'�tre (nous allons l'utiliser
ci-dessous).

Par exemple, pour utiliser le JavaScript YUI Compressor, la configuration
suivante doit �tre ajout�e :

.. configuration-block::

    .. code-block:: yaml

        # app/config/config.yml
        assetic:
            filters:
                yui_js:
                    jar: "%kernel.root_dir%/Resources/java/yuicompressor.jar"

    .. code-block:: xml

        <!-- app/config/config.xml -->
        <assetic:config>
            <assetic:filter
                name="yui_js"
                jar="%kernel.root_dir%/Resources/java/yuicompressor.jar" />
        </assetic:config>

    .. code-block:: php

        // app/config/config.php
        $container->loadFromExtension('assetic', array(
            'filters' => array(
                'yui_js' => array(
                    'jar' => '%kernel.root_dir%/Resources/java/yuicompressor.jar',
                ),
            ),
        ));

Maintenant, pour vraiment *utiliser* le filtre sur un groupe de fichiers, ajoutez
le dans votre template :

.. configuration-block::

    .. code-block:: html+jinja

        {% javascripts
            '@AcmeFooBundle/Resources/public/js/*'
            filter='yui_js'
        %}
        <script src="{{ asset_url }}"></script>
        {% endjavascripts %}

    .. code-block:: html+php

        <?php foreach ($view['assetic']->javascripts(
            array('@AcmeFooBundle/Resources/public/js/*'),
            array('yui_js')) as $url): ?>
        <script src="<?php echo $view->escape($url) ?>"></script>
        <?php endforeach; ?>

Vous pouvez trouver un guide plus d�taill� sur la configuration et l'utilisation
des filtres Assetic ainsi que des informations sur le mode debug d'Assetic
en lisant :doc:`/cookbook/assetic/yuicompressor`.

Contr�ler l'URL utilis�e
------------------------

Si vous le voulez, vous pouvez contr�ler les URLs g�n�r�es par Assetic.
Cela se fait dans le template, et le chemin est relatif par rapport
� la racine publique :

.. configuration-block::

    .. code-block:: html+jinja

        {% javascripts
            '@AcmeFooBundle/Resources/public/js/*'
            output='js/compiled/main.js'
        %}
        <script src="{{ asset_url }}"></script>
        {% endjavascripts %}

    .. code-block:: html+php

        <?php foreach ($view['assetic']->javascripts(
            array('@AcmeFooBundle/Resources/public/js/*'),
            array(),
            array('output' => 'js/compiled/main.js')
        ) as $url): ?>
        <script src="<?php echo $view->escape($url) ?>"></script>
        <?php endforeach; ?>

.. note::

    Symfony contient �galement une m�thode pour le *cache busting* (technique
    emp�chant la mise en cache), o� l'URL g�n�r�e par Assetic contient un
    param�tre qui peut �tre incr�ment�, via la configuration, � chaque
    d�ploiement. Pour plus d'informations, lisez l'option de configuration
    :ref:`ref-framework-assets-version`.

.. _cookbook-assetic-dumping:

Exporter les ressources
-----------------------

En environnement de ``dev``, Assetic g�n�re des chemins vers des fichiers CSS et
JavaScript qui n'existent pas physiquement sur votre ordinateur. Mais ils sont
n�anmoins affich�s car un contr�leur interne de Symfony ouvre les fichiers et
sert leur contenu (apr�s avoir ex�cut� tous les filtres).

Cette mani�re dynamique de servir des ressources trait�es est g�niale car
cela signifie que vous pouvez imm�diatement voir les modifications que vous
apportez � vos fichiers. Mais l'inconv�nient et que cela peut parfois �tre
un peu plus lent. Si vous utilisez beaucoup de filtres, cela peut �tre
carr�ment frustrant.

Heureusement, Assetic fournit une m�thode pour exporter vos ressources vers
des fichiers r�els au lieu de les g�n�rer dynamiquement.


Exporter les ressources en environnement de ``prod``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

En environnement de ``prod``, vos fichiers JS et CSS sont repr�sent�s chacun
par une balise unique. En d'autres termes, plut�t que de voir chacun des fichiers
JavaScript que vous incluez dans votre code source, vous verrez probablement quelque
chose comme ceci :

.. code-block:: html

    <script src="/app_dev.php/js/abcd123.js"></script>

De plus, ce fichier n'existe **pas** vraiment et n'est pas non plus affich�
dynamiquement par Symfony (car les ressources sont en environnement de ``dev``).
C'est fait expr�s : laisser Symfony g�n�rer ces fichiers dynamiquement en production
serait tout simplement trop lent.

Au lieu de cela, chaque fois que vous ex�cutez votre application dans l'environnement
de ``prod`` (et par cons�quent, chaque fois que vous d�ployez), vous devriez lancer
la commande suivante :

.. code-block:: bash

    php app/console assetic:dump --env=prod --no-debug

Cela g�n�rera physiquement et �crira chaque fichier dont vous avez besoin
(ex ``/js/abcd123.js``). Si vous mettez � jour vos ressources, vous aurez besoin
de relancer cette commande pour reg�n�rer vos fichiers.

Exporter les ressources en environnement de ``dev``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Par d�faut, chaque chemin de ressource g�n�r� en environnement de ``dev``
est pris en charge dynamiquement par Symfony. Cela n'a pas d'inconv�nient
(vous pouvez voir vos changements imm�diatement), sauf que les ressources
peuvent �tre charg�es plus lentement. Si vous trouvez que vos ressources sont
charg�s trop lentement, suivez ce guide

Premi�rement, dites � Symfony de ne plus essayer de traiter ces fichiers
dynamiquement. Apportez les modifications suivantes dans le fichier ``config_dev.yml`` :

.. configuration-block::

    .. code-block:: yaml

        # app/config/config_dev.yml
        assetic:
            use_controller: false

    .. code-block:: xml

        <!-- app/config/config_dev.xml -->
        <assetic:config use-controller="false" />

    .. code-block:: php

        // app/config/config_dev.php
        $container->loadFromExtension('assetic', array(
            'use_controller' => false,
        ));

Ensuite, puisque Symfony ne g�n�re plus ces fichiers pour vous, vous
aurez besoin de les exporter manuellement. Pour ce faire, lancez la commande
suivante :

.. code-block:: bash

    php app/console assetic:dump

Elle �crit physiquement tous les fichiers de ressource dont vous avez
besoin pour l'environnement de ``dev``. Le gros inconv�nient est que vous
devrez faire cela chaque fois que vous modifiez une ressource. Heureusement,
en passant l'option ``--watch``, la commande reg�n�rera automatiquement les
ressources *modifi�es* :

.. code-block:: bash

    php app/console assetic:dump --watch

Lancer cette commande en environnement de ``dev`` peut g�n�rer un floril�ge
de fichiers. Pour conserver votre projet bien organis�, il peut �tre int�ressant
de mettre les fichiers g�n�r�s dans un r�pertoire s�par� (ex ``/js/compiled``) :

.. configuration-block::

    .. code-block:: html+jinja

        {% javascripts
            '@AcmeFooBundle/Resources/public/js/*'
            output='js/compiled/main.js'
        %}
        <script src="{{ asset_url }}"></script>
        {% endjavascripts %}

    .. code-block:: html+php

        <?php foreach ($view['assetic']->javascripts(
            array('@AcmeFooBundle/Resources/public/js/*'),
            array(),
            array('output' => 'js/compiled/main.js')
        ) as $url): ?>
        <script src="<?php echo $view->escape($url) ?>"></script>
        <?php endforeach; ?>
