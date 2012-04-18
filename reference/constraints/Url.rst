Url
===

Valide qu'une valeur est une URL valide.

+----------------+---------------------------------------------------------------------+
| S'applique �   | :ref:`propri�t� ou m�thode<validation-property-target>`             |
+----------------+---------------------------------------------------------------------+
| Options        | - `message`_                                                        |
|                | - `protocols`_                                                      |
+----------------+---------------------------------------------------------------------+
| Classe         | :class:`Symfony\\Component\\Validator\\Constraints\\Url`            |
+----------------+---------------------------------------------------------------------+
| Validateur     | :class:`Symfony\\Component\\Validator\\Constraints\\UrlValidator`   |
+----------------+---------------------------------------------------------------------+

Utilisation de base
-------------------

.. configuration-block::

    .. code-block:: yaml

        # src/BlogBundle/Resources/config/validation.yml
        Acme\BlogBundle\Entity\Author:
            properties:
                bioUrl:
                    - Url:

    .. code-block:: php-annotations

       // src/Acme/BlogBundle/Entity/Author.php
       namespace Acme\BlogBundle\Entity;
       
       use Symfony\Component\Validator\Constraints as Assert;

       class Author
       {
           /**
            * @Assert\Url()
            */
            protected $bioUrl;
       }

Options
-------

message
~~~~~~~

**type**: ``string`` **default**: ``This value is not a valid URL``

Le message qui sera affich� si l'URL n'est pas valide.

protocols
~~~~~~~~~

**type**: ``array`` **default**: ``array('http', 'https')``

Cette option d�finit les protocoles consid�r�s comme valides. Par exemple,
si vous avez besoin de consid�rer les URLs du type ``ftp://`` comme valides,
vous devrez red�finir le tableau ``protocols`` en listant ``http``, ``https``,
mais aussi ``ftp``.
