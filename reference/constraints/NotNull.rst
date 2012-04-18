NotNull
=======

Valide qu'une valeur n'est strictement pas �gale � ``null``. Pour vous assurer qu'une
valeur ne soit simplement pas vide (pas une chaine de caract�res vide), lisez la
documentation de la contrainte :doc:`/reference/constraints/NotBlank`.

+----------------+-----------------------------------------------------------------------+
| S'applique �   | :ref:`propri�t� ou m�thode<validation-property-target>`               |
+----------------+-----------------------------------------------------------------------+
| Options        | - `message`_                                                          |
+----------------+-----------------------------------------------------------------------+
| Classe         | :class:`Symfony\\Component\\Validator\\Constraints\\NotNull`          |
+----------------+-----------------------------------------------------------------------+
| Validateur     | :class:`Symfony\\Component\\Validator\\Constraints\\NotNullValidator` |
+----------------+-----------------------------------------------------------------------+

Utilisation de base
-------------------

Si vous voulez vous assurer que la propri�t� ``firstName`` d'une classe ``Author``
ne soit strictement pas �gale � ``null``, ajoutez le code suivant :

.. configuration-block::

    .. code-block:: yaml

        properties:
            firstName:
                - NotNull: ~

    .. code-block:: php-annotations

        // src/Acme/BlogBundle/Entity/Author.php
        use Symfony\Component\Validator\Constraints as Assert;

        class Author
        {
            /**
             * @Assert\NotNull()
             */
            protected $firstName;
        }

Options
-------

message
~~~~~~~

**type**: ``string`` **default**: ``This value should not be null``

Le message qui sera affich� si la valeur est �gale � ``null``.
