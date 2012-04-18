UserPassword
============

.. versionadded:: 2.1

   Cette contrainte n'existe que depuis la version 2.1.

Cette contrainte valide qu'une valeur saisie est �gale au mot de passe
de l'utilisateur courant. C'est utile dans un formulaire o� l'utilisateur
peut changer son mot de passe mais doit d'abord entrer son ancien mot de
passe pour des raisons de s�curit�.

.. note::

    Elle ne devrait *pas* �tre utilis�e dans un formulaire de connexion,
	puisque c'est fait automatiquement par le syst�me de s�curit�.

Lorsqu'elle est appliqu�e � un tableau (ou un objet Traversable), cette contrainte
vous permet d'appliquer une collection de contraintes � chaque �l�ment du tableau.

+----------------+----------------------------------------------------------------------------------------+
| S'applique �   | :ref:`propri�t� ou m�thode<validation-property-target>`                                |
+----------------+----------------------------------------------------------------------------------------+
| Options        | - `message`_                                                                           |
+----------------+----------------------------------------------------------------------------------------+
| Classe         | :class:`Symfony\\Component\\Validator\\Constraints\\UserPassword`                      |
+----------------+----------------------------------------------------------------------------------------+
| Validateur     | :class:`Symfony\\Bundle\\SecurityBundle\\Validator\\Constraint\\UserPasswordValidator` |
+----------------+----------------------------------------------------------------------------------------+

Utilisation de base
-------------------

Supposons que vous avez une classe `PasswordChange` qui est utilis�e dans un
formulaire o� l'utilisateur peut changer son mot de passe en entrant son
ancien mot de passe et son nouveau mot de passe. Cette contrainte validera
que l'ancien mot de passe est correct :

.. configuration-block::

    .. code-block:: yaml

        # src/UserBundle/Resources/config/validation.yml
        Acme\UserBundle\Form\Model\ChangePassword:
            properties:
                oldPassword:
                    - UserPassword:
                        message: "Votre mot de passe actuel est erron�"

    .. code-block:: php-annotations

       // src/Acme/UserBundle/Form/Model/ChangePassword.php
       namespace Acme\UserBundle\Form\Model;
       
       use Symfony\Component\Validator\Constraints as Assert;

       class ChangePassword
       {
           /**
            * @Assert\UserPassword(
            *     message = "Votre mot de passe actuel est erron�"
            * )
            */
            protected $oldPassword;
       }

Options
-------

message
~~~~~~~

**type**: ``message`` **default**: ``This value should be the user current password``

Le message qui sera affich� si la chaine de caract�res ne correspond *pas*
au mot de passe actuel de l'utilisateur.
