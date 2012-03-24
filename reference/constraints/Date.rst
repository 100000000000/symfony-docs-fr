Date
====

Valide qu'une valeur est une date valide, c'est-�-dire soit un objet ``DateTime``,
soit une chaine de caract�res (ou un objet qui peut �tre converti en chaine de caract�res)
qui respecte un format valide YYYY-MM-DD.


+----------------+--------------------------------------------------------------------+
| S'applique �   | :ref:`propri�t� ou m�thode<validation-property-target>`            |
+----------------+--------------------------------------------------------------------+
| Options        | - `message`_                                                       |
+----------------+--------------------------------------------------------------------+
| Classe         | :class:`Symfony\\Component\\Validator\\Constraints\\Date`          |
+----------------+--------------------------------------------------------------------+
| Validateur     | :class:`Symfony\\Component\\Validator\\Constraints\\DateValidator` |
+----------------+--------------------------------------------------------------------+

Utilisation de base
-------------------

.. configuration-block::

    .. code-block:: yaml

        # src/Acme/BlogBundle/Resources/config/validation.yml
        Acme\BlogBundle\Entity\Author:
            properties:
                birthday:
                    - Date: ~

    .. code-block:: php-annotations

        // src/Acme/BlogBundle/Entity/Author.php
        use Symfony\Component\Validator\Constraints as Assert;

        class Author
        {
            /**
             * @Assert\Date()
             */
             protected $birthday;
        }

Options
-------

message
~~~~~~~

**type**: ``string`` **default**: ``This value is not a valid date``

Ce message s'affiche si la donn�e finale n'est pas une date valide.
