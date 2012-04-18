File
====

Valide qu'une valeur est un � fichier � valide, qui peut �tre l'un des formats
suivants :

* Une chaine de caract�res (ou un objet avec une m�thode ``__toString()``) qui
   repr�sente un chemin vers un fichier existant;

* Un objet :class:`Symfony\\Component\\HttpFoundation\\File\\File` valide
  (ce qui inclut les objets de la classe :class:`Symfony\\Component\\HttpFoundation\\File\\UploadedFile`).

Cette contrainte est souvent utilis�e dans les formulaires avec le type de champ
:doc:`file</reference/forms/types/file>`.

.. tip::

    Si le fichier que vous validez est une image, essayez la contrainte
    :doc:`Image</reference/constraints/Image>`.

+----------------+---------------------------------------------------------------------+
| S'applique �   | :ref:`propri�t� ou m�thode<validation-property-target>`             |
+----------------+---------------------------------------------------------------------+
| Options        | - `maxSize`_                                                        |
|                | - `mimeTypes`_                                                      |
|                | - `maxSizeMessage`_                                                 |
|                | - `mimeTypesMessage`_                                               |
|                | - `notFoundMessage`_                                                |
|                | - `notReadableMessage`_                                             |
|                | - `uploadIniSizeErrorMessage`_                                      |
|                | - `uploadFormSizeErrorMessage`_                                     |
|                | - `uploadErrorMessage`_                                             |
+----------------+---------------------------------------------------------------------+
| Classe         | :class:`Symfony\\Component\\Validator\\Constraints\\File`           |
+----------------+---------------------------------------------------------------------+
| Validateur     | :class:`Symfony\\Component\\Validator\\Constraints\\FileValidator`  |
+----------------+---------------------------------------------------------------------+

Utilisation de base
-------------------

Cette contrainte est souvent utilis�e sur une propri�t� qui est affich�e dans
un formulaire avec le type de champ :doc:`file</reference/forms/types/file>`.
Par exemple, supposons que vous cr�ez un formulaire Auteur o� vous pouvez
uploader une � bio � au format PDF. Dans votre formulaire, la propri�t�
``bioFile`` sera un type ``file``. La classe ``Author`` ressemblerait � ceci::

    // src/Acme/BlogBundle/Entity/Author.php
    namespace Acme\BlogBundle\Entity;

    use Symfony\Component\HttpFoundation\File\File;

    class Author
    {
        protected $bioFile;

        public function setBioFile(File $file = null)
        {
            $this->bioFile = $file;
        }

        public function getBioFile()
        {
            return $this->bioFile;
        }
    }

Pour garantir que l'objet ``File`` ``bioFile`` soit valide, et que le fichier
soit plus petit qu'une certaine taille et soit au format PDF, ajoutez le code
suivant :

.. configuration-block::

    .. code-block:: yaml

        # src/Acme/BlogBundle/Resources/config/validation.yml
        Acme\BlogBundle\Entity\Author
            properties:
                bioFile:
                    - File:
                        maxSize: 1024k
                        mimeTypes: [application/pdf, application/x-pdf]
                        mimeTypesMessage: Choisissez un fichier PDF valide
                        

    .. code-block:: php-annotations

        // src/Acme/BlogBundle/Entity/Author.php
        use Symfony\Component\Validator\Constraints as Assert;

        class Author
        {
            /**
             * @Assert\File(
             *     maxSize = "1024k",
             *     mimeTypes = {"application/pdf", "application/x-pdf"},
             *     mimeTypesMessage = "Choisissez un fichier PDF valide"
             * )
             */
            protected $bioFile;
        }

    .. code-block:: xml

        <!-- src/Acme/BlogBundle/Resources/config/validation.xml -->
        <class name="Acme\BlogBundle\Entity\Author">
            <property name="bioFile">
                <constraint name="File">
                    <option name="maxSize">1024k</option>
                    <option name="mimeTypes">
                        <value>application/pdf</value>
                        <value>application/x-pdf</value>
                    </option>
                    <option name="mimeTypesMessage">Choisissez un fichier PDF valide</option>
                </constraint>
            </property>
        </class>

    .. code-block:: php

        // src/Acme/BlogBundle/Entity/Author.php
        // ...

        use Symfony\Component\Validator\Mapping\ClassMetadata;
        use Symfony\Component\Validator\Constraints\File;

        class Author
        {
            // ...

            public static function loadValidatorMetadata(ClassMetadata $metadata)
            {
                $metadata->addPropertyConstraint('bioFile', new File(array(
                    'maxSize' => '1024k',
                    'mimeTypes' => array(
                        'application/pdf',
                        'application/x-pdf',
                    ),
                    'mimeTypesMessage' => 'Choisissez un fichier PDF valide',
                )));
            }
        }

La propri�t� ``bioFile`` est valid�e pour garantir qu'il s'agisse bien d'un
fichier. Sa taille et son type MIME sont �galement valid�s car les options
correspondantes ont �t� sp�cifi�es.

Options
-------

maxSize
~~~~~~~

**type**: ``mixed``

Si cette option est d�finie, la taille du fichier doit �tre inf�rieure � la taille
sp�cifi�e pour �tre valide. La taille du fichier peut �tre donn�e dans l'un des formats
suivants :

* **octets**: Pour sp�cifier l'option ``maxSize`` en octets, entrez la valeur en num�rique
  seulement (ex ``4096``);

* **kilooctets**: Pour sp�cifier l'option ``maxSize`` en kilooctets, entrez la valeur num�rique
  et ajoutez le suffixe � k � en minuscule (ex ``200k``);

* **megaoctet**: Pour sp�cifier l'option ``maxSize`` en megaoctets, entrez la valeur num�rique
  et ajoutez le suffixe � M � en majuscule (ex ``200M``);

mimeTypes
~~~~~~~~~

**type**: ``array`` ou ``string``

Si elle cette option est d�finie, le validateur v�rifiera que le type MIME
du fichier envoy� correspond au type MIME donn� (s'il est d�fini sous forme
de chaine de caract�res) ou s'il existe dans la collection de types MIME
donn�s (s'ils sont d�finis comme tableau).

maxSizeMessage
~~~~~~~~~~~~~~

**type**: ``string`` **default**: ``The file is too large ({{ size }}). Allowed maximum size is {{ limit }}``

Le message affich� si le fichier upload� est plus lourd que l'option `maxSize`_.

mimeTypesMessage
~~~~~~~~~~~~~~~~

**type**: ``string`` **default**: ``The mime type of the file is invalid ({{ type }}). Allowed mime types are {{ types }}``

Le message affich� si le type MIME du fichier ne correspond pas au(x) type(s) MIME
autoris�(s) par l'option `mimeTypes`_.

notFoundMessage
~~~~~~~~~~~~~~~

**type**: ``string`` **default**: ``The file could not be found``

Le message affich� si aucun fichier ne correspond au chemin donn�. Cette
erreur n'est possible que si la valeur sous-jacente est un chemin sous forme
de chaine de caract�res, puisque l'objet ``File`` ne pourra pas �tre construit � partir
d'un chemin invalide.

notReadableMessage
~~~~~~~~~~~~~~~~~~

**type**: ``string`` **default**: ``The file is not readable``

Le message affich� si le fichier existe, mais que la fonction PHP ``is_readable``
�choue � passer le chemin au fichier.

uploadIniSizeErrorMessage
~~~~~~~~~~~~~~~~~~~~~~~~~

**type**: ``string`` **default**: ``The file is too large. Allowed maximum size is {{ limit }}``

Le message affich� si le fichier upload� est plus lourd que le maximum d�fini dans le param�tre
``upload_max_filesize`` du PHP.ini.

uploadFormSizeErrorMessage
~~~~~~~~~~~~~~~~~~~~~~~~~~

**type**: ``string`` **default**: ``The file is too large``

Le message affich� si le fichier upload� est plus lourd que le maximum
autoris� dans champ HTML input file.

uploadErrorMessage
~~~~~~~~~~~~~~~~~~

**type**: ``string`` **default**: ``The file could not be uploaded``

Le message affich� si le fichier ne peut pas �tre upload� pour une raison
quelconque, par exemple si l'upload �choue ou qu'il est impossible d'�crire
sur le disque.