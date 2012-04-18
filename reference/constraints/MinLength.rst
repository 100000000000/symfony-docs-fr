MinLength
=========

Valide que la longueur d'une chaine de caract�res est au moins sup�rieure � la
limite donn�e.

+----------------+-------------------------------------------------------------------------+
| S'applique �   | :ref:`propri�t� ou m�thode<validation-property-target>`                 |
+----------------+-------------------------------------------------------------------------+
| Options        | - `limit`_                                                              |
|                | - `message`_                                                            |
|                | - `charset`_                                                            |
+----------------+-------------------------------------------------------------------------+
| Classe         | :class:`Symfony\\Component\\Validator\\Constraints\\MinLength`          |
+----------------+-------------------------------------------------------------------------+
| Validateur     | :class:`Symfony\\Component\\Validator\\Constraints\\MinLengthValidator` |
+----------------+-------------------------------------------------------------------------+

Utilisation de base
-------------------

.. configuration-block::

    .. code-block:: yaml

        # src/Acme/BlogBundle/Resources/config/validation.yml
        Acme\BlogBundle\Entity\Blog:
            properties:
                firstName:
                    - MinLength: { limit: 3, message: "Votre nom doit faire au moins {{ limit }} caract�res." }

    .. code-block:: php-annotations

        // src/Acme/BlogBundle/Entity/Blog.php
        use Symfony\Component\Validator\Constraints as Assert;

        class Blog
        {
            /**
             * @Assert\MinLength(
             *     limit=3,
             *     message="Votre nom doit faire au moins {{ limit }} caract�res."
             * )
             */
            protected $summary;
        }

    .. code-block:: xml

        <!-- src/Acme/BlogBundle/Resources/config/validation.xml -->
        <class name="Acme\BlogBundle\Entity\Blog">
            <property name="summary">
                <constraint name="MinLength">
                    <option name="limit">3</option>
                    <option name="message">Votre nom doit faire au moins {{ limit }} caract�res.</option>
                </constraint>
            </property>
        </class>

Options
-------

limit
~~~~~

**type**: ``integer`` [:ref:`default option<validation-default-option>`]

Cette option obligatoire est la valeur � minimale�. La validation �chouera
si la longueur de la chaine de caract�res donn�e est **inf�rieure** � ce
nombre.

message
~~~~~~~

**type**: ``string`` **default**: ``This value is too short. It should have {{ limit }} characters or more``

Le message qui sera affich� si la longueur de la chaine de caract�res est
inf�rieure � l'option `limit`_.

charset
~~~~~~~

**type**: ``charset`` **default**: ``UTF-8``


Si l'extension PHP � mbstring � est install�e, alors la fonction PHP `mb_strlen`_
sera utilis�e pour calculer la longueur de la chaine. La valeur de l'option
``charset`` est pass�e comme second argument de cette fonction.

.. _`mb_strlen`: http://php.net/manual/fr/function.mb-strlen.php
