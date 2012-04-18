Valid
=====

Cette contrainte est utilis�e pour activer la validation sur les objets
imbriqu�s dans un objet qui doit �tre valid�. Cela vous permet de valider
un objet et les sous-objets qui lui sont associ�s.

+----------------+---------------------------------------------------------------------+
| S'applique �   | :ref:`propri�t� ou m�thode<validation-property-target>`             |
+----------------+---------------------------------------------------------------------+
| Options        | - `traverse`_                                                       |
+----------------+---------------------------------------------------------------------+
| Classe         | :class:`Symfony\\Component\\Validator\\Constraints\\Type`           |
+----------------+---------------------------------------------------------------------+

Utilisation de base
-------------------

Dans l'exemple suivant, nous cr�ons deux classes ``Author`` et ``Address``
qui ont toutes les deux des contraintes sur leurs propri�t�s. De plus, 
l'objet ``Author`` stocke une instance d'``Address`` dans sa propri�t� ``$address``.

.. code-block:: php

    // src/Acme/HelloBundle/Address.php
    class Address
    {
        protected $street;
        protected $zipCode;
    }

.. code-block:: php

    // src/Acme/HelloBundle/Author.php
    class Author
    {
        protected $firstName;
        protected $lastName;
        protected $address;
    }

.. configuration-block::

    .. code-block:: yaml

        # src/Acme/HelloBundle/Resources/config/validation.yml
        Acme\HelloBundle\Address:
            properties:
                street:
                    - NotBlank: ~
                zipCode:
                    - NotBlank: ~
                    - MaxLength: 5

        Acme\HelloBundle\Author:
            properties:
                firstName:
                    - NotBlank: ~
                    - MinLength: 4
                lastName:
                    - NotBlank: ~

    .. code-block:: xml

        <!-- src/Acme/HelloBundle/Resources/config/validation.xml -->
        <class name="Acme\HelloBundle\Address">
            <property name="street">
                <constraint name="NotBlank" />
            </property>
            <property name="zipCode">
                <constraint name="NotBlank" />
                <constraint name="MaxLength">5</constraint>
            </property>
        </class>

        <class name="Acme\HelloBundle\Author">
            <property name="firstName">
                <constraint name="NotBlank" />
                <constraint name="MinLength">4</constraint>
            </property>
            <property name="lastName">
                <constraint name="NotBlank" />
            </property>
        </class>

    .. code-block:: php-annotations

        // src/Acme/HelloBundle/Address.php
        use Symfony\Component\Validator\Constraints as Assert;

        class Address
        {
            /**
             * @Assert\NotBlank()
             */
            protected $street;

            /**
             * @Assert\NotBlank
             * @Assert\MaxLength(5)
             */
            protected $zipCode;
        }

        // src/Acme/HelloBundle/Author.php
        class Author
        {
            /**
             * @Assert\NotBlank
             * @Assert\MinLength(4)
             */
            protected $firstName;

            /**
             * @Assert\NotBlank
             */
            protected $lastName;
            
            protected $address;
        }

    .. code-block:: php

        // src/Acme/HelloBundle/Address.php
        use Symfony\Component\Validator\Mapping\ClassMetadata;
        use Symfony\Component\Validator\Constraints\NotBlank;
        use Symfony\Component\Validator\Constraints\MaxLength;
        
        class Address
        {
            protected $street;

            protected $zipCode;
            
            public static function loadValidatorMetadata(ClassMetadata $metadata)
            {
                $metadata->addPropertyConstraint('street', new NotBlank());
                $metadata->addPropertyConstraint('zipCode', new NotBlank());
                $metadata->addPropertyConstraint('zipCode', new MaxLength(5));
            }
        }

        // src/Acme/HelloBundle/Author.php
        use Symfony\Component\Validator\Mapping\ClassMetadata;
        use Symfony\Component\Validator\Constraints\NotBlank;
        use Symfony\Component\Validator\Constraints\MinLength;
        
        class Author
        {
            protected $firstName;

            protected $lastName;
            
            protected $address;
            
            public static function loadValidatorMetadata(ClassMetadata $metadata)
            {
                $metadata->addPropertyConstraint('firstName', new NotBlank());
                $metadata->addPropertyConstraint('firstName', new MinLength(4));
                $metadata->addPropertyConstraint('lastName', new NotBlank());
            }
        }

Avec cette configuration, il est possible de valider un auteur dont l'adresse serait
incorrecte. Pour �viter ceci, ajouter la contrainte ``Valid`` � la propri�t�
``$address``.

.. configuration-block::

    .. code-block:: yaml

        # src/Acme/HelloBundle/Resources/config/validation.yml
        Acme\HelloBundle\Author:
            properties:
                address:
                    - Valid: ~

    .. code-block:: xml

        <!-- src/Acme/HelloBundle/Resources/config/validation.xml -->
        <class name="Acme\HelloBundle\Author">
            <property name="address">
                <constraint name="Valid" />
            </property>
        </class>

    .. code-block:: php-annotations

        // src/Acme/HelloBundle/Author.php
        use Symfony\Component\Validator\Constraints as Assert;

        class Author
        {
            /* ... */
            
            /**
             * @Assert\Valid
             */
            protected $address;
        }

    .. code-block:: php

        // src/Acme/HelloBundle/Author.php
        use Symfony\Component\Validator\Mapping\ClassMetadata;
        use Symfony\Component\Validator\Constraints\Valid;
        
        class Author
        {
            protected $address;
            
            public static function loadValidatorMetadata(ClassMetadata $metadata)
            {
                $metadata->addPropertyConstraint('address', new Valid());
            }
        }

Maintenant, si vous validez un auteur avec une adresse incorrecte, vous verrez
que la validation du champ ``Address`` �chouera.

    Acme\HelloBundle\Author.address.zipCode:
    Cette valeur est trop longue. 5 caract�res maximum sont autoris�s

Options
-------

traverse
~~~~~~~~

**type**: ``string`` **default**: ``true``

Si cette contrainte est appliqu�e � une propri�t� qui contient un tableau
d'objets, alors chaque objet du tableau sera valid� si cette option est
d�finie � ``true``.
