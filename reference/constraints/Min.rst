Min
===

Valide qu'un nombre donn� est *sup�rieur* � un nombre minimum.

+----------------+--------------------------------------------------------------------+
| S'applique �   | :ref:`propri�t� ou m�thode<validation-property-target>`            |
+----------------+--------------------------------------------------------------------+
| Options        | - `limit`_                                                         |
|                | - `message`_                                                       |
|                | - `invalidMessage`_                                                |
+----------------+--------------------------------------------------------------------+
| Classe         | :class:`Symfony\\Component\\Validator\\Constraints\\Min`           |
+----------------+--------------------------------------------------------------------+
| Validateur     | :class:`Symfony\\Component\\Validator\\Constraints\\MinValidator`  |
+----------------+--------------------------------------------------------------------+

Utilisation de base
-------------------

Pour v�rifier qu'un champ � �ge � d'une classe est sup�rieur ou �gal � � 18 �,
vous pourriez utiliser le code suivant :

.. configuration-block::

    .. code-block:: yaml

        # src/Acme/EventBundle/Resources/config/validation.yml
        Acme\EventBundle\Entity\Participant:
            properties:
                age:
                    - Min: { limit: 18, message: Vous devez avoir au moins 18 ans pour entrer. }

    .. code-block:: php-annotations

        // src/Acme/EventBundle/Entity/Participant.php
        use Symfony\Component\Validator\Constraints as Assert;

        class Participant
        {
            /**
             * @Assert\Min(limit = "18", message = "Vous devez avoir au moins 18 ans pour entrer")
             */
             protected $age;
        }

Options
-------

limit
~~~~~

**type**: ``integer`` [:ref:`default option<validation-default-option>`]

Cette option obligatoire est la valeur � minimale �. La validation �chouera
si la valeur donn�e est **inf�rieure** � cette valeur minimale.

message
~~~~~~~

**type**: ``string`` **default**: ``This value should be {{ limit }} or more``

Le message qui sera affich� si la valeur est inf�rieure � l'option `limit`_.

invalidMessage
~~~~~~~~~~~~~~

**type**: ``string`` **default**: ``This value should be a valid number``

Le message qui sera affich� si la valeur soumise n'est pas un nombre (pour la fonction
PHP `is_numeric`_).

.. _`is_numeric`: http://www.php.net/manual/fr/function.is-numeric.php