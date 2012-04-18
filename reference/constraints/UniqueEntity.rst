UniqueEntity
============

Valide qu'un champ particulier (ou plusieurs champs) d'une entit� Doctrine sont
uniques.
C'est souvent utilis�, par exemple, pour �viter qu'un nouvel utilisateur ne
s'enregistre avec une adresse email qui existe d�j� dans le syst�me.

+----------------+-------------------------------------------------------------------------------------+
| S'applique �   | :ref:`classe<validation-class-target>`                                              |
+----------------+-------------------------------------------------------------------------------------+
| Options        | - `fields`_                                                                         |
|                | - `message`_                                                                        |
|                | - `em`_                                                                             |
+----------------+-------------------------------------------------------------------------------------+
| Classe         | :class:`Symfony\\Bridge\\Doctrine\\Validator\\Constraints\\UniqueEntity`            |
+----------------+-------------------------------------------------------------------------------------+
| Validateur     | :class:`Symfony\\Bridge\\Doctrine\\Validator\\Constraints\\UniqueEntity\\Validator` |
+----------------+-------------------------------------------------------------------------------------+

Utilisation de base
-------------------

Supposons que vous avez un ``AcmeUserBundle`` avec une entit� ``User`` qui
a un champ ``email``. Vous pouvez utiliser la contrainte ``Unique`` pour garantir
que le champ ``email``soit unique dans votre table d'utilisateurs :

.. configuration-block::

    .. code-block:: php-annotations

        // Acme/UserBundle/Entity/User.php
        use Symfony\Component\Validator\Constraints as Assert;
        use Doctrine\ORM\Mapping as ORM;

        // N'OUBLIEZ pas d'inclure ce use !
        use Symfony\Bridge\Doctrine\Validator\Constraints\UniqueEntity;

        /**
         * @ORM\Entity
         * @UniqueEntity("email")
         */
        class Author
        {
            /**
             * @var string $email
             *
             * @ORM\Column(name="email", type="string", length=255, unique=true)
             * @Assert\Email()
             */
            protected $email;
            
            // ...
        }

    .. code-block:: yaml

        # src/Acme/UserBundle/Resources/config/validation.yml
        Acme\UserBundle\Entity\Author:
            constraints:
                - Symfony\Bridge\Doctrine\Validator\Constraints\UniqueEntity: email
            properties:
                email:
                    - Email: ~

    .. code-block:: xml

        <class name="Acme\UserBundle\Entity\Author">
            <constraint name="Symfony\Bridge\Doctrine\Validator\Constraints\UniqueEntity">
                <option name="fields">email</option>
                <option name="message">Cet email existe d�j�.</option>
            </constraint>
             <property name="email">
                <constraint name="Email" />
            </property>
        </class>

Options
-------

fields
~~~~~~

**type**: ``array``|``string`` [:ref:`default option<validation-default-option>`]

Cette option obligatoire est le champ (ou la liste de champs) qui sont
uniques pour l'entit�. Par exemple, vous pouvez sp�cifier que les champs
email et nom d'un utilisateur doivent �tre uniques.

message
~~~~~~~

**type**: ``string`` **default**: ``This value is already used.``

Le message qui sera affich� si la validation �choue.

em
~~

**type**: ``string``

Le nom du gestionnaire d'entit� (entity manager) � utiliser pour faire la
requ�te qui d�terminera l'unicit�. Si elle est vide, le gestionnaire sera
d�termin� automatiquement pour cette classe. Pour cette raison, vous n'aurez
probablement pas besoin d'utiliser cette option.
