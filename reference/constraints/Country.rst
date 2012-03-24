Country
=======

Valide qu'une valeur est un code de pays en deux-lettres. 

+----------------+------------------------------------------------------------------------+
| S'applique �   | :ref:`propri�t� ou m�thode<validation-property-target>`                |
+----------------+------------------------------------------------------------------------+
| Options        | - `message`_                                                           |
+----------------+------------------------------------------------------------------------+
| Classe         | :class:`Symfony\\Component\\Validator\\Constraints\\Country`           |
+-----------------------------------------------------------------------------------------+
| Validateur     | :class:`Symfony\\Component\\Validator\\Constraints\\CountryValidator`  |
+----------------+------------------------------------------------------------------------+

Utilisation de base
-------------------

.. configuration-block::

    .. code-block:: yaml

        # src/UserBundle/Resources/config/validation.yml
        Acme\UserBundle\Entity\User:
            properties:
                country:
                    - Country:

    .. code-block:: php-annotations

       // src/Acme/UserBundle/Entity/User.php
       namespace Acme\UserBundle\Entity;
       
       use Symfony\Component\Validator\Constraints as Assert;

       class User
       {
           /**
            * @Assert\Country
            */
            protected $country;
       }

Options
-------

message
~~~~~~~

**type**: ``string`` **default**: ``This value is not a valid country``

Ce message s'affiche si la chaine de caract�res n'est pas un code pays valide.
