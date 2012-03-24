DateTime
========

Valide que la valeur est un � datetime � valide, c'est-�-dire soit un objet
``DateTime``, soit une chaine de caract�res (ou un objet qui peut �tre converti
en chaine de caract�res) qui respecte un format YYYY-MM-DD HH:MM:SS valide.

+----------------+------------------------------------------------------------------------+
| S'applique �   | :ref:`propri�t� ou m�thode<validation-property-target>`                |
+----------------+------------------------------------------------------------------------+
| Options        | - `message`_                                                           |
+----------------+------------------------------------------------------------------------+
| Classe         | :class:`Symfony\\Component\\Validator\\Constraints\\DateTime`          |
+----------------+------------------------------------------------------------------------+
| Validateur     | :class:`Symfony\\Component\\Validator\\Constraints\\DateTimeValidator` |
+----------------+------------------------------------------------------------------------+

Utilisation de base
-------------------

.. configuration-block::

    .. code-block:: yaml

        # src/Acme/BlogBundle/Resources/config/validation.yml
        Acme\BlogBundle\Entity\Author:
            properties:
                createdAt:
                    - DateTime: ~

    .. code-block:: php-annotations

        // src/Acme/BlogBundle/Entity/Author.php
        namespace Acme\BlogBundle\Entity;

        use Symfony\Component\Validator\Constraints as Assert;

        class Author
        {
            /**
             * @Assert\DateTime()
             */
             protected $createdAt;
        }

Options
-------

message
~~~~~~~

**type**: ``string`` **default**: ``This value is not a valid datetime``

Le message est affich� si la donn�es finale c'est pas un datetime.
