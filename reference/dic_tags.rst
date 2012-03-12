Les Tags de l'Injection de D�pendances
======================================

Tags:

* ``data_collector``
* ``form.type``
* ``form.type_extension``
* ``form.type_guesser``
* ``kernel.cache_warmer``
* ``kernel.event_listener``
* ``kernel.event_subscriber``
* ``monolog.logger``
* ``monolog.processor``
* ``templating.helper``
* ``routing.loader``
* ``translation.loader``
* ``twig.extension``
* ``validator.initializer``

Activer les helpers de template PHP personnalis�s
-------------------------------------------------

Pour activer un helper de template personnalis�, ajoutez le en tant que
service dans votre configuration, taggez le avec ``templating.helper`` et
d�finissez l'attribut ``alias`` (le helper sera accessible par cet alias dans
vos templates) :

.. configuration-block::

    .. code-block:: yaml

        services:
            templating.helper.your_helper_name:
                class: Fully\Qualified\Helper\Class\Name
                tags:
                    - { name: templating.helper, alias: alias_name }

    .. code-block:: xml

        <service id="templating.helper.your_helper_name" class="Fully\Qualified\Helper\Class\Name">
            <tag name="templating.helper" alias="alias_name" />
        </service>

    .. code-block:: php

        $container
            ->register('templating.helper.your_helper_name', 'Fully\Qualified\Helper\Class\Name')
            ->addTag('templating.helper', array('alias' => 'alias_name'))
        ;

.. _reference-dic-tags-twig-extension:

Activer une extension Twig personnalis�e
----------------------------------------

Pour activer une extension Twig, ajoutez la comme service dans votre
configuration et taggez la avec ``twig.extension`` :

.. configuration-block::

    .. code-block:: yaml

        services:
            twig.extension.your_extension_name:
                class: Fully\Qualified\Extension\Class\Name
                tags:
                    - { name: twig.extension }

    .. code-block:: xml

        <service id="twig.extension.your_extension_name" class="Fully\Qualified\Extension\Class\Name">
            <tag name="twig.extension" />
        </service>

    .. code-block:: php

        $container
            ->register('twig.extension.your_extension_name', 'Fully\Qualified\Extension\Class\Name')
            ->addTag('twig.extension')
        ;

Pour plus d'informations sur comment cr�er une classe d'Extension Twig, lisez
la `documentation Twig`_ sur le sujet.

Avant d'�crire votre propre extension, jetez un oeil au
`d�p�t officiel des extensions Twig`_ qui contient d�j� plusieurs extensions
tr�s utiles. Par exemple ``Intl`` et ses filtres ``localizeddate`` qui formattent
une date selon la locale de l'utilisateur. Ces extensions Twig officielles ont
�galement besoin d'�tre ajout�es comme services :

.. configuration-block::

    .. code-block:: yaml

        services:
            twig.extension.intl:
                class: Twig_Extensions_Extension_Intl
                tags:
                    - { name: twig.extension }

    .. code-block:: xml

        <service id="twig.extension.intl" class="Twig_Extensions_Extension_Intl">
            <tag name="twig.extension" />
        </service>

    .. code-block:: php

        $container
            ->register('twig.extension.intl', 'Twig_Extensions_Extension_Intl')
            ->addTag('twig.extension')
        ;

.. _dic-tags-kernel-event-listener:

Activer des listeners personnalis�s
-----------------------------------

Pour activer un listener personnalis�, ajoutez le comme service dans 
votre configuration et taggez le avec ``kernel.event_listener``. Vous devez
d�finir le nom de l'�v�nement que votre service �coute, ainsi que la m�thode
qui sera appel�e :

.. configuration-block::

    .. code-block:: yaml

        services:
            kernel.listener.your_listener_name:
                class: Fully\Qualified\Listener\Class\Name
                tags:
                    - { name: kernel.event_listener, event: xxx, method: onXxx }

    .. code-block:: xml

        <service id="kernel.listener.your_listener_name" class="Fully\Qualified\Listener\Class\Name">
            <tag name="kernel.event_listener" event="xxx" method="onXxx" />
        </service>

    .. code-block:: php

        $container
            ->register('kernel.listener.your_listener_name', 'Fully\Qualified\Listener\Class\Name')
            ->addTag('kernel.event_listener', array('event' => 'xxx', 'method' => 'onXxx'))
        ;

.. note::

    Vous pouvez aussi sp�cifier l'attribut priority du tag kernel.event_listener 
    (tout comme les attributs method ou event) avec un entier positif ou n�gatif.
	Cela vous permet d'�tre s�r que votre listener sera toujours appel� avant ou
	apr�s un autre listener qui �coute le m�me �v�nement.

.. _dic-tags-kernel-event-subscriber:

Activer les abonnements personnalis�s
-------------------------------------

.. versionadded:: 2.1
   
   La possibilit� d'ajouter des abonnements � un �v�nement du noyau est une nouveaut�
   de la version 2.1.

Pour activer un abonnement personnalis�, ajoutez le comme service dans votre configuration
et taggez le avec ``kernel.event_subscriber`` :

.. configuration-block::

    .. code-block:: yaml

        services:
            kernel.subscriber.your_subscriber_name:
                class: Fully\Qualified\Subscriber\Class\Name
                tags:
                    - { name: kernel.event_subscriber }

    .. code-block:: xml

        <service id="kernel.subscriber.your_subscriber_name" class="Fully\Qualified\Subscriber\Class\Name">
            <tag name="kernel.event_subscriber" />
        </service>

    .. code-block:: php

        $container
            ->register('kernel.subscriber.your_subscriber_name', 'Fully\Qualified\Subscriber\Class\Name')
            ->addTag('kernel.event_subscriber')
        ;

.. note::

    Votre service doit impl�menter l'interface :class:`Symfony\Component\EventDispatcher\EventSubscriberInterface`.

.. note::

    Si votre service est cr�� par une factory, vous *DEVEZ* d�finir correctement
    le param�tre ``class`` pour que ce tag fonctionne bien.

Activer les moteurs de template personnalis�s
---------------------------------------------

Pour activer un moteur de template personnalis�, ajoutez le comme service
dans votre configuration, et taggez le avec ``templating.engine`` :

.. configuration-block::

    .. code-block:: yaml

        services:
            templating.engine.your_engine_name:
                class: Fully\Qualified\Engine\Class\Name
                tags:
                    - { name: templating.engine }

    .. code-block:: xml

        <service id="templating.engine.your_engine_name" class="Fully\Qualified\Engine\Class\Name">
            <tag name="templating.engine" />
        </service>

    .. code-block:: php

        $container
            ->register('templating.engine.your_engine_name', 'Fully\Qualified\Engine\Class\Name')
            ->addTag('templating.engine')
        ;

Activer un chargeur de route personnalis�
-----------------------------------------

Pour ajouter un chargeur de route personnalis�, ajoutez le comme service dans
votre configuration et taggez le avec ``routing.loader``:

.. configuration-block::

    .. code-block:: yaml

        services:
            routing.loader.your_loader_name:
                class: Fully\Qualified\Loader\Class\Name
                tags:
                    - { name: routing.loader }

    .. code-block:: xml

        <service id="routing.loader.your_loader_name" class="Fully\Qualified\Loader\Class\Name">
            <tag name="routing.loader" />
        </service>

    .. code-block:: php

        $container
            ->register('routing.loader.your_loader_name', 'Fully\Qualified\Loader\Class\Name')
            ->addTag('routing.loader')
        ;

.. _dic_tags-monolog:

Utiliser un canal d'authentification personnalis� avec Monolog
--------------------------------------------------------------

Monolog vous permet de partager ses gestionnaires entre plusieurs canaux
d'authentification. Le service logger utilise le canal ``app``
mais vous pouvez changer de canal en l'injectant dans le service.

.. configuration-block::

    .. code-block:: yaml

        services:
            my_service:
                class: Fully\Qualified\Loader\Class\Name
                arguments: [@logger]
                tags:
                    - { name: monolog.logger, channel: acme }

    .. code-block:: xml

        <service id="my_service" class="Fully\Qualified\Loader\Class\Name">
            <argument type="service" id="logger" />
            <tag name="monolog.logger" channel="acme" />
        </service>

    .. code-block:: php

        $definition = new Definition('Fully\Qualified\Loader\Class\Name', array(new Reference('logger'));
        $definition->addTag('monolog.logger', array('channel' => 'acme'));
        $container->register('my_service', $definition);;

.. note::

    Ce ne fonctionne que quand le service logger est un argument du constructeur,
    pas quand il est inject� avec un setter.

.. _dic_tags-monolog-processor:

Ajouter un processeur pour Monolog
----------------------------------

Monolog vous permet d'ajouter des processeurs dans le logger ou dans les 
gestionnaires pour ajouter des donn�es suppl�mentaires � l'enregistrement.
Un processeur recoit l'enregistrement comme argument et doit le retourner
apr�s avoir ajout� des donn�es suppl�mentaires dans l'attribut ``extra`` de
l'enregistrement.

Regardons comment vous pouvez utiliser le processeur pr�construit ``IntrospectionProcessor``
pour ajouter le fichier, la ligne, la classe et la m�thode o� le logger a �t� d�clench�.

Vous pouvez ajouter un processeur de fa�on globale :

.. configuration-block::

    .. code-block:: yaml

        services:
            my_service:
                class: Monolog\Processor\IntrospectionProcessor
                tags:
                    - { name: monolog.processor }

    .. code-block:: xml

        <service id="my_service" class="Monolog\Processor\IntrospectionProcessor">
            <tag name="monolog.processor" />
        </service>

    .. code-block:: php

        $definition = new Definition('Monolog\Processor\IntrospectionProcessor');
        $definition->addTag('monolog.processor');
        $container->register('my_service', $definition);

.. tip::
    Si votre service n'est pas appelable directement (en utilisant ``__invoke``), vous
    pouvez ajouter l'attribut ``method`` dans le tag pour utiliser une m�thode sp�cifique.

vous pouvez ajouter aussi un processeur pour un gestionnaire sp�cifique en utilisant
l'attribut ``handler`` :

.. configuration-block::

    .. code-block:: yaml

        services:
            my_service:
                class: Monolog\Processor\IntrospectionProcessor
                tags:
                    - { name: monolog.processor, handler: firephp }

    .. code-block:: xml

        <service id="my_service" class="Monolog\Processor\IntrospectionProcessor">
            <tag name="monolog.processor" handler="firephp" />
        </service>

    .. code-block:: php

        $definition = new Definition('Monolog\Processor\IntrospectionProcessor');
        $definition->addTag('monolog.processor', array('handler' => 'firephp');
        $container->register('my_service', $definition);

Vous pouvez �galement ajouter un processuer pour un canal d'authentification sp�cifique
en utilisant l'attribut ``channel``. Cela enregistrera le processeur uniquement pour le canal d'authentification ``security`` qui est utilis� dans le composant Security :

.. configuration-block::

    .. code-block:: yaml

        services:
            my_service:
                class: Monolog\Processor\IntrospectionProcessor
                tags:
                    - { name: monolog.processor, channel: security }

    .. code-block:: xml

        <service id="my_service" class="Monolog\Processor\IntrospectionProcessor">
            <tag name="monolog.processor" channel="security" />
        </service>

    .. code-block:: php

        $definition = new Definition('Monolog\Processor\IntrospectionProcessor');
        $definition->addTag('monolog.processor', array('channel' => 'security');
        $container->register('my_service', $definition);

.. note::

    Vous ne pouvez pas utiliser les attributs ``handler`` et ``channel`` simultann�ment
    dans un m�me tag car les gestionnaires sont partag�s avec tous les canaux.

..  _`documentation Twig`: http://twig.sensiolabs.org/doc/extensions.html
..  _`d�p�t officiel des extensions Twig`: http://github.com/fabpot/Twig-extensions
