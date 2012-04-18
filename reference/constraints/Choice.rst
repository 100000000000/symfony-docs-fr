Choice
======

Cette contrainte est utilis�e pour s'assurer qu'une valeur donn�e fait partie
d'un ensemble de choix *valides*. Elle peut aussi �tre utilis�e pour valider
que chaque item d'un tableau d'items est l'un des choix valides.

+----------------+-----------------------------------------------------------------------+
| S'applique �   | :ref:`propri�t� ou m�thode<validation-property-target>`               |
+----------------+-----------------------------------------------------------------------+
| Options        | - `choices`_                                                          |
|                | - `callback`_                                                         |
|                | - `multiple`_                                                         |
|                | - `min`_                                                              |
|                | - `max`_                                                              |
|                | - `message`_                                                          |
|                | - `multipleMessage`_                                                  |
|                | - `minMessage`_                                                       |
|                | - `maxMessage`_                                                       |
|                | - `strict`_                                                           |
+----------------+-----------------------------------------------------------------------+
| Classe         | :class:`Symfony\\Component\\Validator\\Constraints\\Choice`           |
+----------------+-----------------------------------------------------------------------+
| Validateur     | :class:`Symfony\\Component\\Validator\\Constraints\\ChoiceValidator`  |
+----------------+-----------------------------------------------------------------------+

Utilisation de base
-------------------

L'id�e principale de cette contrainte est que fournissez un tableau de valeurs
valides (cela peut �tre fait de diff�rentes mani�res) et elle valide que la
valeur d'une propri�t� donn�es est bien dans ce tableau.

Si votre liste de choix valides est simple, vous pouvez la passer directement
via l'option `choices`_ :

.. configuration-block::

    .. code-block:: yaml

        # src/Acme/BlogBundle/Resources/config/validation.yml
        Acme\BlogBundle\Entity\Author:
            properties:
                gender:
                    - Choice:
                        choices:  [male, female]
                        message:  Choisissez un sexe valide.

    .. code-block:: xml

        <!-- src/Acme/BlogBundle/Resources/config/validation.xml -->
        <class name="Acme\BlogBundle\EntityAuthor">
            <property name="gender">
                <constraint name="Choice">
                    <option name="choices">
                        <value>male</value>
                        <value>female</value>
                    </option>
                    <option name="message">Choisissez un sexe valide.</option>
                </constraint>
            </property>
        </class>

    .. code-block:: php-annotations

        // src/Acme/BlogBundle/Entity/Author.php
        use Symfony\Component\Validator\Constraints as Assert;

        class Author
        {
            /**
             * @Assert\Choice(choices = {"male", "female"}, message = "Choisissez un sexe valide.")
             */
            protected $gender;
        }

    .. code-block:: php

        // src/Acme/BlogBundle/EntityAuthor.php
        use Symfony\Component\Validator\Mapping\ClassMetadata;
        use Symfony\Component\Validator\Constraints\Choice;
        
        class Author
        {
            protected $gender;
            
            public static function loadValidatorMetadata(ClassMetadata $metadata)
            {
                $metadata->addPropertyConstraint('gender', new Choice(array(
                    'choices' => array('male', 'female'),
                    'message' => 'Choisissez un sexe valide.',
                )));
            }
        }

Fournir les choix par une fonction callback
-------------------------------------------

Vous pouvez aussi utiliser une fonction callback pour sp�cifier vos options. C'est
utile si vous voulez garder vos choix dans un endroit centralis� pour, par exemple,
avoir acc�s facilement � ces choix pour la validation ou pour construire des listes
d�roulantes pour les formulaires.

.. code-block:: php

    // src/Acme/BlogBundle/Entity/Author.php
    class Author
    {
        public static function getGenders()
        {
            return array('male', 'female');
        }
    }

Vous pouvez passer le nom de cette m�thode � l'option `callback_` de la contrainte
``Choice``.

.. configuration-block::

    .. code-block:: yaml

        # src/Acme/BlogBundle/Resources/config/validation.yml
        Acme\BlogBundle\Entity\Author:
            properties:
                gender:
                    - Choice: { callback: getGenders }

    .. code-block:: php-annotations

        // src/Acme/BlogBundle/Entity/Author.php
        use Symfony\Component\Validator\Constraints as Assert;

        class Author
        {
            /**
             * @Assert\Choice(callback = "getGenders")
             */
            protected $gender;
        }

    .. code-block:: xml

        <!-- src/Acme/BlogBundle/Resources/config/validation.xml -->
        <class name="Acme\BlogBundle\Entity\Author">
            <property name="gender">
                <constraint name="Choice">
                    <option name="callback">getGenders</option>
                </constraint>
            </property>
        </class>

Si le callback statique est stock� dans une classe diff�rente, par exemple
``Util``, vous pouvez passer le nom de la classe et la m�thode dans un tableau.

.. configuration-block::

    .. code-block:: yaml

        # src/Acme/BlogBundle/Resources/config/validation.yml
        Acme\BlogBundle\Entity\Author:
            properties:
                gender:
                    - Choice: { callback: [Util, getGenders] }

    .. code-block:: xml

        <!-- src/Acme/BlogBundle/Resources/config/validation.xml -->
        <class name="Acme\BlogBundle\Entity\Author">
            <property name="gender">
                <constraint name="Choice">
                    <option name="callback">
                        <value>Util</value>
                        <value>getGenders</value>
                    </option>
                </constraint>
            </property>
        </class>

    .. code-block:: php-annotations

        // src/Acme/BlogBundle/Entity/Author.php
        use Symfony\Component\Validator\Constraints as Assert;

        class Author
        {
            /**
             * @Assert\Choice(callback = {"Util", "getGenders"})
             */
            protected $gender;
        }

Options disponibles
-------------------

choices
~~~~~~~

**type**: ``array`` [:ref:`default option<validation-default-option>`]
Cette option obligatoire (� moins que `callback`_ soit sp�cifi�e)
repr�sente le tableau d'options qui doit �tre consid�r� comme un
ensemble valide. La donn�e soumise sera compar�e � ce tableau.

callback
~~~~~~~~

**type**: ``string|array|Closure``

C'est la m�thode callback qui peut �tre utilis�e au lieu de l'option `choices`_
pour retourner le tableau de choix. Lisez `Fournir les choix par une fonction callback`_
pour plus d'informations sur son utilisation.

multiple
~~~~~~~~

**type**: ``Boolean`` **default**: ``false``

Si cette option est d�finie � true, la valeur soumise attendue est un tableau
et non plus une simple valeur. La contrainte v�rifiera que chaque valeur du tableau
soumis se trouve dans le tableau de choix valides. Si une seule des valeurs soumises
n'est pas trouv�e, la validation �chouera.

min
~~~

**type**: ``integer``

Si l'option ``multiple`` est � true, alors vous pouvez utiliser l'option ``min``
pour forcer qu'au moins XX valeurs doivent �tre s�lectionn�es. Par exemple,
si ``min`` vaut 3 et si le tableau soumis contient 2 items valides, la validation
�chouera.

max
~~~

**type**: ``integer``

Si l'option ``multiple`` est � true, alors vous pouvez utiliser l'option ``max``
pour forcer que XX valeurs peuvent �tre s�lectionn�es au maximum. Par exemple,
si ``max`` vaut 3 et si le tableau soumis contient 4 items valides, la validation
�chouera.

message
~~~~~~~

**type**: ``string`` **default**: ``The value you selected is not a valid choice``

C'est le message que vous verrez si l'option ``multiple`` est d�finie � ``false``,
et que la valeur soumise n'est pas dans le tableau de choix valides.

multipleMessage
~~~~~~~~~~~~~~~

**type**: ``string`` **default**: ``One or more of the given values is invalid``

C'est le message que vous verrez si l'option ``multiple`` est d�finie � ``true``,
et que l'une des valeurs du tableau soumis n'est pas dans le tableau de valeurs
valides.

minMessage
~~~~~~~~~~

**type**: ``string`` **default**: ``You must select at least {{ limit }} choices``

C'est le message d'erreur qui est affich� quand l'utilisateur choisit trop peu de choix
(en fonction de l'option `min`_).

maxMessage
~~~~~~~~~~

**type**: ``string`` **default**: ``You must select at most {{ limit }} choices``

C'est le message d'erreur qui est affich� quand l'utilisateur choisit trop de choix
(en fonction de l'option `max`_).

strict
~~~~~~

**type**: ``Boolean`` **default**: ``false``

Si cette option est � true, le validateur v�rifiera �galement le type de la donn�e soumise.
Sp�cifiquement, cette valeur est pass�e comme troisi�me argument de la m�thode PHP `in_array`_
lorsque vous v�rifiez qu'une valeur est bien dans le tableau de choix valides.

.. _`in_array`: http://php.net/manual/en/function.in-array.php
