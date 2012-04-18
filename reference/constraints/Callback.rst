Callback
========

Le but de l'assertion Callback est de vous permettre de cr�er enti�rement des
r�gles de validation personnalis�es et d'assigner des erreurs de validation �
des champs sp�cifiques de votre objet. Si vous utilisez la validation de formulaires,
cela signifie que vous pouvez faire en sorte que ces erreurs personnalis�es s'affichent
� c�t� d'un champ sp�cifique plut�t qu'en haut de votre formulaire.

Cela fonctionne en sp�cifiant des m�thodes *callback*, chacune d'elles �tant appel�e
durant le processus de validation. Chacune de ces m�thode peut faire toute
sorte de choses, incluant la cr�ation et l'assignation d'erreurs de validation.

.. note::
    
	Une m�thode callback elle-m�me n'*�choue* pas et ne retourne aucune valeur.
	Au lieu de cela, comme vous le verrez dans l'exemple, cette m�thode a le
	pouvoir d'ajouter directement des � violations � de validateur.

+----------------+------------------------------------------------------------------------+
| S'applique �   | :ref:`classe<validation-class-target>`                                  |
+----------------+------------------------------------------------------------------------+
| Options        | - `methods`_                                                           |
+----------------+------------------------------------------------------------------------+
| Classe         | :class:`Symfony\\Component\\Validator\\Constraints\\Callback`          |
+----------------+------------------------------------------------------------------------+
| Validateur     | :class:`Symfony\\Component\\Validator\\Constraints\\CallbackValidator` |
+----------------+------------------------------------------------------------------------+

Configuration
-------------

.. configuration-block::

    .. code-block:: yaml

        # src/Acme/BlogBundle/Resources/config/validation.yml
        Acme\BlogBundle\Entity\Author:
            constraints:
                - Callback:
                    methods:   [isAuthorValid]

    .. code-block:: xml

        <!-- src/Acme/BlogBundle/Resources/config/validation.xml -->
        <class name="Acme\BlogBundle\Entity\Author">
            <constraint name="Callback">
                <option name="methods">
                    <value>isAuthorValid</value>
                </option>
            </constraint>
        </class>

    .. code-block:: php-annotations

        // src/Acme/BlogBundle/Entity/Author.php
        use Symfony\Component\Validator\Constraints as Assert;

        /**
         * @Assert\Callback(methods={"isAuthorValid"})
         */
        class Author
        {
        }

La m�thode Callback
-------------------

Un objet sp�cial ``ExecutionContext`` est pass� � la m�thode callback. Vous
pouvez d�finir des � violations � directement sur cet objet et d�terminer �
quel champ ces erreurs seront attribu�es::

    // ...
    use Symfony\Component\Validator\ExecutionContext;
    
    class Author
    {
        // ...
        private $firstName;
    
        public function isAuthorValid(ExecutionContext $context)
        {
            // Vous avez un tableau de � faux noms �
            $fakeNames = array();
        
            // v�rifie si le nom est un faux
            if (in_array($this->getFirstName(), $fakeNames)) {
                $context->addViolationAtSubPath('firstname', 'This name sounds totally fake!', array(), null);
            }
        }

Options
-------

methods
~~~~~~~

**type**: ``array`` **default**: ``array()`` [:ref:`option par d�faut<validation-default-option>`]

Il s'agit d'un tableau de m�thodes qui doivent �tre ex�cut�es durant le
processus de validation. Chacune de ces m�thodes peut avoir l'un des formats
suivants :

1) **Nom de la m�thode en chaine de caract�res**

    Si le nom de la m�thode est une simple chaine de caract�res (ex ``isAuthorValid``), cette
	m�thode sera appel�e sur le m�me objet que celui qui est en train d'�tre valid�
	et ``ExecutionContext`` sera le seul argument (voyez l'exemple ci-dessus).

2) **Tableau statique**

    Chaque m�thode peut �galement �tre sp�cifi�e sous forme de tableau standard :

    .. configuration-block::

        .. code-block:: yaml

            # src/Acme/BlogBundle/Resources/config/validation.yml
            Acme\BlogBundle\Entity\Author:
                constraints:
                    - Callback:
                        methods:
                            -    [Acme\BlogBundle\MyStaticValidatorClass, isAuthorValid]

        .. code-block:: php-annotations

            // src/Acme/BlogBundle/Entity/Author.php
            use Symfony\Component\Validator\Constraints as Assert;

            /**
             * @Assert\Callback(methods={
             *     { "Acme\BlogBundle\MyStaticValidatorClass", "isAuthorValid"}
             * })
             */
            class Author
            {
            }

        .. code-block:: php

            // src/Acme/BlogBundle/Entity/Author.php

            use Symfony\Component\Validator\Mapping\ClassMetadata;
            use Symfony\Component\Validator\Constraints\Callback;

            class Author
            {
                public $name;

                public static function loadValidatorMetadata(ClassMetadata $metadata)
                {
                    $metadata->addConstraint(new Callback(array(
                        'methods' => array('isAuthorValid'),
                    )));
                }
            }
    
	Dans ce cas, la m�thode statique ``isAuthorValid`` sera appel�e sur la classe
    ``Acme\BlogBundle\MyStaticValidatorClass``. Deux objets sont pass�s en param�tre,
    l'objet en cours de validation (ex ``Author``) et le ``ExecutionContext``::

        namespace Acme\BlogBundle;
    
        use Symfony\Component\Validator\ExecutionContext;
        use Acme\BlogBundle\Entity\Author;
    
        class MyStaticValidatorClass
        {
            static public function isAuthorValid(Author $author, ExecutionContext $context)
            {
                // ...
            }
        }

    .. tip::
        
		Si vous sp�cifiez votre contrainte ``Callback`` via PHP, alors vous avez
		�galement le choix de faire votre callback en closure PHP, ou en non statique.
		Il n'est, en revanche, *pas* possible de sp�cifier un :term:`service` comme
		contrainte. Pour valider en utilisant un service, vous devriez
        :doc:`cr�er une contrainte de validation personnalis�e</cookbook/validation/custom_constraint>`
        et ajouter cette nouvelle contrainte � votre classe.
