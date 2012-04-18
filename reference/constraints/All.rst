All
===

Quand elle est appliqu�e � un tableau (ou un objet Traversable), cette contrainte vous
permet d'appliquer un ensemble de contraintes � chaque �l�ment du tableau.

+----------------+------------------------------------------------------------------------+
| S'applique �   | :ref:`propri�t� ou m�thode<validation-property-target>`                |
+----------------+------------------------------------------------------------------------+
| Options        | - `constraints`_                                                       |
+----------------+------------------------------------------------------------------------+
| Classe         | :class:`Symfony\\Component\\Validator\\Constraints\\All`               |
+----------------+------------------------------------------------------------------------+
| Validateur     | :class:`Symfony\\Component\\Validator\\Constraints\\AllValidator`      |
+----------------+------------------------------------------------------------------------+

Utilisation de base
-------------------

Supposons que vous avez un tableau de chaines de caract�res, et que vous
voulez valider chaque entr�e du tableau :

.. configuration-block::

    .. code-block:: yaml

        # src/UserBundle/Resources/config/validation.yml
        Acme\UserBundle\Entity\User:
            properties:
                favoriteColors:
                    - All:
                        - NotBlank:  ~
                        - MinLength: 5

    .. code-block:: php-annotations

       // src/Acme/UserBundle/Entity/User.php
       namespace Acme\UserBundle\Entity;
       
       use Symfony\Component\Validator\Constraints as Assert;

       class User
       {
           /**
            * @Assert\All({
            *     @Assert\NotBlank
            *     @Assert\MinLength(5),
            * })
            */
            protected $favoriteColors = array();
       }

Maintenant, chaque entr�e du tableau ``favoriteColors`` sera valid�e
pour ne pas �tre vide et faire au moins 5 caract�res.

Options
-------

constraints
~~~~~~~~~~~

**type**: ``array`` [:ref:`default option<validation-default-option>`]

Cette option obligatoire est le tableau de contraintes de validation que
vous voulez appliquer � chaque �l�ment du tableau sous-jacent.
