Time
====

Valide qu'une valeur est une heure valide, c'est-�-dire soit un objet ``DateTime``,
soit une chaine de caract�res (ou un objet converti en chaine de caract�res) qui 
respecte un format � HH:MM:SS � valide.

+----------------+------------------------------------------------------------------------+
| S'applique �   | :ref:`propri�t� ou m�thode<validation-property-target>`                |
+----------------+------------------------------------------------------------------------+
| Options        | - `message`_                                                           |
+----------------+------------------------------------------------------------------------+
| Classe         | :class:`Symfony\\Component\\Validator\\Constraints\\Time`              |
+----------------+------------------------------------------------------------------------+
| Validateur     | :class:`Symfony\\Component\\Validator\\Constraints\\TimeValidator`     |
+----------------+------------------------------------------------------------------------+

Utilisation de base
-------------------

Supposons que vous avez une classe Event, avec un champ ``startAt`` qui est
l'heure � laquelle l'�v�nement commence :

.. configuration-block::

    .. code-block:: yaml

        # src/Acme/EventBundle/Resources/config/validation.yml
        Acme\EventBundle\Entity\Event:
            properties:
                startsAt:
                    - Time: ~

    .. code-block:: php-annotations

        // src/Acme/EventBundle/Entity/Event.php
        namespace Acme\EventBundle\Entity;
        
        use Symfony\Component\Validator\Constraints as Assert;

        class Event
        {
            /**
             * @Assert\Time()
             */
             protected $startsAt;
        }

Options
-------

message
~~~~~~~

**type**: ``string`` **default**: ``This value is not a valid time``

Le message qui est affich� si la donn�e n'est pas une heure valide.
