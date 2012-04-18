Regex
=====

Valide qu'une valeur correspond � une expression r�guli�re.

+----------------+-----------------------------------------------------------------------+
| S'applique �   | :ref:`propri�t� ou m�thode<validation-property-target>`               |
+----------------+-----------------------------------------------------------------------+
| Options        | - `pattern`_                                                          |
|                | - `match`_                                                            |
|                | - `message`_                                                          |
+----------------+-----------------------------------------------------------------------+
| Classe         | :class:`Symfony\\Component\\Validator\\Constraints\\Regex`            |
+----------------+-----------------------------------------------------------------------+
| Validateur     | :class:`Symfony\\Component\\Validator\\Constraints\\RegexValidator`   |
+----------------+-----------------------------------------------------------------------+

Utilisation de base
-------------------

Supposons que vous avez un champ ``description`` et que vous voulez v�rifier
qu'il commence bien par un caract�re alphabnum�rique. L'expression r�guli�re
qui teste cela serait ``/^\w+/``, indiquant que vous cherchez au moins un ou
plusieurs caract�res alphanum�riques au d�but de votre chaine :

.. configuration-block::

    .. code-block:: yaml

        # src/Acme/BlogBundle/Resources/config/validation.yml
        Acme\BlogBundle\Entity\Author:
            properties:
                description:
                    - Regex: "/^\w+/"

    .. code-block:: php-annotations

        // src/Acme/BlogBundle/Entity/Author.php
        namespace Acme\BlogBundle\Entity;
        
        use Symfony\Component\Validator\Constraints as Assert;

        class Author
        {
            /**
             * @Assert\Regex("/^\w+/")
             */
            protected $description;
        }

Alternativement, vous pouvez d�finir l'option `match`_ � ``false`` pour
v�rifier qu'une chaine donn�e ne correspond *pas*. Dans l'exemple suivant,
vous v�rifiez que le champ ``firstName`` ne contient pas de nombre et vous
personnalisez �galement le message :

.. configuration-block::

    .. code-block:: yaml

        # src/Acme/BlogBundle/Resources/config/validation.yml
        Acme\BlogBundle\Entity\Author:
            properties:
                firstName:
                    - Regex:
                        pattern: "/\d/"
                        match:   false
                        message: Votre nom ne peux pas contenir de nombre

    .. code-block:: php-annotations

        // src/Acme/BlogBundle/Entity/Author.php
        namespace Acme\BlogBundle\Entity;
        
        use Symfony\Component\Validator\Constraints as Assert;

        class Author
        {
            /**
             * @Assert\Regex(
             *     pattern="/\d/",
             *     match=false,
             *     message="Votre nom ne peux pas contenir de nombre"
             * )
             */
            protected $firstName;
        }

Options
-------

pattern
~~~~~~~

**type**: ``string`` [:ref:`default option<validation-default-option>`]

Cette option obligatoire est le masque (pattern) de l'expression r�guli�re
� laquelle doit correspondre la donn�e. Par d�faut, le validateur �chouera
si la chaine de caract�res *ne correspond pas* � cette expression r�guli�re
(via la fonction PHP `preg_match`_).
Toutefois, si l'option `match`_ est d�finie � false, la validation �chouera
si la chaine *correspond* � l'expression r�guli�re.

match
~~~~~

**type**: ``Boolean`` default: ``true``

Si cette option est � ``true`` (ou non d�finie), la validation passera si la chaine
donn�e correspond au `pattern`_ de l'expression r�guli�re. Toutefois, si cette option
est d�finir � ``false``, l'inverse se passera : la validation passera uniquement si
la chaine donn�e ne correspond **pas** au `pattern`_ de l'expression r�guli�re.

message
~~~~~~~

**type**: ``string`` **default**: ``This value is not valid``

Le message qui sera affich� si la validation �choue.

.. _`preg_match`: http://php.net/manual/fr/function.preg-match.php
