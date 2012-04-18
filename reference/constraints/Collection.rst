Collection
==========

Cette contrainte est utilis�e lorsque l'objet sous-jacent est une collection
(c'est-�-dire un tableau ou un objet qui impl�mentent ``Traversable`` et ``ArrayAccess``),
mais vous aimeriez valider les diff�rentes cl�s de cette collection de diff�rentes
mani�res. Par exemple, vous pourriez valider la cl� ``email`` en utilisant la contrainte
``Email`` et la cl� ``inventory`` avec la contrainte ``Min``.

Cette contrainte permet �galement de s'assurer que certaines cl�s de la collection
sont bien pr�sente et que des cl�s suppl�mentaires ne le sont pas.

+----------------+--------------------------------------------------------------------------+
| S'applique �   | :ref:`propri�t� ou m�thode<validation-property-target>`                  |
+----------------+--------------------------------------------------------------------------+
| Options        | - `fields`_                                                              |
|                | - `allowExtraFields`_                                                    |
|                | - `extraFieldsMessage`_                                                  |
|                | - `allowMissingFields`_                                                  |
|                | - `missingFieldsMessage`_                                                |
+----------------+--------------------------------------------------------------------------+
| Classe         | :class:`Symfony\\Component\\Validator\\Constraints\\Collection`          |
+----------------+--------------------------------------------------------------------------+
| Validateur     | :class:`Symfony\\Component\\Validator\\Constraints\\CollectionValidator` |
+----------------+--------------------------------------------------------------------------+

Utilisation de base
-------------------

La contrainte ``Collection`` vous permet de valider les diff�rentes cl�s
d'une collection individuellement. Prenez l'exemple suivant::

    namespace Acme\BlogBundle\Entity;
    
    class Author
    {
        protected $profileData = array(
            'personal_email',
            'short_bio',
        );

        public function setProfileData($key, $value)
        {
            $this->profileData[$key] = $value;
        }
    }

Pour valider que l'�l�ment ``personal_email`` de la propri�t� ``profileData``
soit une adresse email valide et que l'�lement ``short_bio`` soit rempli
et d'une longueur de moins de 100 caract�res, vous pouvez proc�der comme ceci :

.. configuration-block::

    .. code-block:: yaml

        properties:
            profileData:
                - Collection:
                    fields:
                        personal_email: Email
                        short_bio:
                            - NotBlank
                            - MaxLength:
                                limit:   100
                                message: Votre bio est trop longue!
                    allowMissingfields: true

    .. code-block:: php-annotations

        // src/Acme/BlogBundle/Entity/Author.php
        use Symfony\Component\Validator\Constraints as Assert;

        class Author
        {
            /**
             * @Assert\Collection(
             *     fields = {
             *         "personal_email" = @Assert\Email,
             *         "short_bio" = {
             *             @Assert\NotBlank(),
             *             @Assert\MaxLength(
             *                 limit = 100,
             *                 message = "Votre bio est trop longue!"
             *             )
             *         }
             *     },
             *     allowMissingfields = true
             * )
             */
             protected $profileData = array(
                 'personal_email',
                 'short_bio',
             );
        }

    .. code-block:: xml

        <!-- src/Acme/BlogBundle/Resources/config/validation.xml -->
        <class name="Acme\BlogBundle\Entity\Author">
            <property name="profileData">
                <constraint name="Collection">
                    <option name="fields">
                        <value key="personal_email">
                            <constraint name="Email" />
                        </value>
                        <value key="short_bio">
                            <constraint name="NotBlank" />
                            <constraint name="MaxLength">
                                <option name="limit">100</option>
                                <option name="message">Votre bio est trop longue!</option>
                            </constraint>
                        </value>
                    </option>
                    <option name="allowMissingFields">true</option>
                </constraint>
            </property>
        </class>

    .. code-block:: php

        // src/Acme/BlogBundle/Entity/Author.php
        use Symfony\Component\Validator\Mapping\ClassMetadata;
        use Symfony\Component\Validator\Constraints\Collection;
        use Symfony\Component\Validator\Constraints\Email;
        use Symfony\Component\Validator\Constraints\MaxLength;

        class Author
        {
            private $options = array();

            public static function loadValidatorMetadata(ClassMetadata $metadata)
            {
                $metadata->addPropertyConstraint('profileData', new Collection(array(
                    'fields' => array(
                        'personal_email' => new Email(),
                        'lastName' => array(new NotBlank(), new MaxLength(100)),
                    ),
                    'allowMissingFields' => true,
                )));
            }
        }

Pr�sence et Absence de champs
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Par d�faut, cette contrainte valide plus que le simple fait que les champs
individuels de la collection respectent leurs contraintes respectives.
En fait, si des cl�s de la collection sont manquantes, ou s'il y a des cl�s
non reconnues, une erreur de validation sera affich�e.

Si vous voulez autoriser des cl�s � �tre absentes de la collection  ou si vous
voulez autoriser des cl�s � extra � (en plus), vous pouvez modifier respectivement
les options `allowMissingFields`_ et `allowExtraFields`_. Dans l'exemple ci-dessus,
l'option ``allowMissingFields`` a �t� d�finie � true, ce qui veut dire que si
l'un des �lements ``personal_email`` ou ``short_bio`` �tait manquant dans la
propri�t� ``$personalData``, aucune erreur de validation ne se serait produite.

Options
-------

fields
~~~~~~

**type**: ``array`` [:ref:`default option<validation-default-option>`]

Cette option est requise et est un tableau associatif qui d�finit toutes les
cl�s de la collection et, pour chaque cl�, quel(s) validateur(s) doit �tre
ex�cut�.

allowExtraFields
~~~~~~~~~~~~~~~~

**type**: ``Boolean`` **default**: false

Si cette option est d�finie � ``false`` et que la collection contient un ou plusieurs
�l�ments qui ne sont pas inclus dans l'option `fields`_, une erreur de validation sera
retourn�e. Si elle est d�finie � ``true``, les champs en plus seront tol�r�s.

extraFieldsMessage
~~~~~~~~~~~~~~~~~~

**type**: ``Boolean`` **default**: ``The fields {{ fields }} were not expected``

Le message affich� si `allowExtraFields`_ est � false et que des champs suppl�mentaires
sont d�tect�s.

allowMissingFields
~~~~~~~~~~~~~~~~~~

**type**: ``Boolean`` **default**: false

Si cette option est d�finie � ``false`` et qu'un ou plusieurs champs de l'option `fields`_
sont manquants, une erreur de validation sera retourn�e. Si elle est d�finie � ``true``,
ce n'est pas grave si des champs de l'option `fields_` sont absents de la collection.

missingFieldsMessage
~~~~~~~~~~~~~~~~~~~~

**type**: ``Boolean`` **default**: ``The fields {{ fields }} are missing``

Le message affich� si `allowMissingFields`_ est � false et qu'un ou plusieurs champs
sont absents de la collection.