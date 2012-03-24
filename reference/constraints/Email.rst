Email
=====

Valide que la valeur est une adresse email valide. La donn�e finale est convertie
en une chaine de caract�res avant d'�tre valid�e.

+----------------+---------------------------------------------------------------------+
| S'applique �   | :ref:`property or method<validation-property-target>`               |
+----------------+---------------------------------------------------------------------+
| Options        | - `message`_                                                        |
|                | - `checkMX`_                                                        |
+----------------+---------------------------------------------------------------------+
| Classe         | :class:`Symfony\\Component\\Validator\\Constraints\\Email`          |
+----------------+---------------------------------------------------------------------+
| Validateur     | :class:`Symfony\\Component\\Validator\\Constraints\\EmailValidator` |
+----------------+---------------------------------------------------------------------+

Utilisation de base
-------------------

.. configuration-block::

    .. code-block:: yaml

        # src/BlogBundle/Resources/config/validation.yml
        Acme\BlogBundle\Entity\Author:
            properties:
                email:
                    - Email:
                        message: "{{ value }}" n'est pas un email valide.
                        checkMX: true

    .. code-block:: php-annotations

        // src/Acme/BlogBundle/Entity/Author.php
        namespace Acme\BlogBundle\Entity;
        
        use Symfony\Component\Validator\Constraints as Assert;

        class Author
        {
            /** 
             * @Assert\Email(
             *     message = "'{{ value }}' n'est pas un email valide.",
             *     checkMX = true
             * )
             */
             protected $email;
        }

Options
-------

message
~~~~~~~

**type**: ``string`` **default**: ``This value is not a valid email address``

Ce message s'affiche si la donn�e finale n'est pas une adresse email valide.

checkMX
~~~~~~~

**type**: ``Boolean`` **default**: ``false``

Si cette option est d�finie � true, alors la fonction PHP `checkdnsrr`_ sera utilis�e
pour v�rifier la validit� du registrement MX du serveur de l'email donn�.

.. _`checkdnsrr`: http://www.php.net/manual/fr/function.checkdnsrr.php