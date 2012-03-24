Blank
=====

Valide qu'une valeur est vide, �gale � une chaine vide, ou �gale � ``null``.
Pour forcer cette valeur � �tre strictement �gale � ``null``, jetez un oeil �
la contrainte :doc:`/reference/constraints/Null`. Pour forcer cette valeur �
ne *pas* �tre vide, lisez :doc:`/reference/constraints/NotBlank`.

+----------------+-----------------------------------------------------------------------+
| S'applique �   | :ref:`propri�t� ou m�thode<validation-property-target>`               |
+----------------+-----------------------------------------------------------------------+
| Options        | - `message`_                                                          |
+----------------+-----------------------------------------------------------------------+
| Classe         | :class:`Symfony\\Component\\Validator\\Constraints\\Blank`            |
+----------------+-----------------------------------------------------------------------+
| Validateur     | :class:`Symfony\\Component\\Validator\\Constraints\\BlankValidator`   |
+----------------+-----------------------------------------------------------------------+

Utilisation de base
-------------------

Si, pour certaines raison, vous voulez vous assurer que la la propri�t� ``firstName``
de la classe ``Author`` soit nulle, vous pouvez proc�der comme ceci :

.. configuration-block::

    .. code-block:: yaml

        properties:
            firstName:
                - Blank: ~

    .. code-block:: php-annotations

        // src/Acme/BlogBundle/Entity/Author.php
        use Symfony\Component\Validator\Constraints as Assert;

        class Author
        {
            /**
             * @Assert\Blank()
             */
            protected $firstName;
        }

Options
-------

message
~~~~~~~

**type**: ``string`` **default**: ``This value should be blank``

Ce message s'affiche si la valeur n'est pas vide.
