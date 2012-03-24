False
=====

Valide que la valeur est ``false``. Sp�cifiquement, cette contrainte v�rifie que la
valeur est exactement ``false``, exactement l'entier ``0``, ou exactement la chaine
de caract�res � ``0`` �.

Vous pouvez �galement voir :doc:`True <True>`.

+----------------+---------------------------------------------------------------------+
| S'applique �   | :ref:`propri�t� ou m�thode<validation-property-target>`             |
+----------------+---------------------------------------------------------------------+
| Options        | - `message`_                                                        |
+----------------+---------------------------------------------------------------------+
| Classe         | :class:`Symfony\\Component\\Validator\\Constraints\\False`          |
+----------------+---------------------------------------------------------------------+
| Validateur     | :class:`Symfony\\Component\\Validator\\Constraints\\FalseValidator` |
+----------------+---------------------------------------------------------------------+

Utilisation de base
-------------------

La contrainte ``False`` s'applique � une propri�t� ou � une m�thode � getter � mais
elle est le plus souvent utilis�e dans le dernier cas. Par exemple, supposons 
que vous voulez garantir qu'une propri�t� ``state`` n'est *pas* dans un tableau
dynamique ``invalidStates``. Premi�rement, vous cr�erez une m�thode � getter �::

    protected $state;

    protectd $invalidStates = array();

    public function isStateInvalid()
    {
        return in_array($this->state, $this->invalidStates);
    }

Dans ce cas, l'objet sous-jacent n'est valide que si la m�thode ``isStateInvalid``
retourne **false** :

.. configuration-block::

    .. code-block:: yaml

        # src/BlogBundle/Resources/config/validation.yml
        Acme\BlogBundle\Entity\Author
            getters:
                stateInvalid:
                    - "False":
                        message: Vous avez saisi un �tat non valide.

    .. code-block:: php-annotations

        // src/Acme/BlogBundle/Entity/Author.php
        use Symfony\Component\Validator\Constraints as Assert;

        class Author
        {
            /**
             * @Assert\False()
             */
             public function isStateInvalid($message = "Vous avez saisi un �tat non valide.")
             {
                // ...
             }
        }

.. caution::

    Si vous utilisez YAML, assurez vous de bien mettre les guillemets autour de
	``False`` (``"False"``), sinon YAML le convertira en Bool�en.

Options
-------

message
~~~~~~~

**type**: ``string`` **default**: ``This value should be false``

Ce message s'affiche si la donn�es n'est pas � false.
