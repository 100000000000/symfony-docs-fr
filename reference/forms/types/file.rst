.. index::
   single: Forms; Fields; file

Le type de champ File
=====================

Le type ``file`` repr�sente un input File dans votre formulaire.

+-------------+---------------------------------------------------------------------+
| Rendu comme | Champ ``input`` ``file``                                            |
+-------------+---------------------------------------------------------------------+
| Options     | - `required`_                                                       |
| h�rit�es    | - `label`_                                                          |
|             | - `read_only`_                                                      |
|             | - `error_bubbling`_                                                 |
+-------------+---------------------------------------------------------------------+
| Type parent | :doc:`form</reference/forms/types/field>`                           |
+-------------+---------------------------------------------------------------------+
| Classe      | :class:`Symfony\\Component\\Form\\Extension\\Core\\Type\\FileType`  |
+-------------+---------------------------------------------------------------------+

Utilisation de base
-------------------

Imaginons que vous avez d�fini ce formulaire :

.. code-block:: php

    $builder->add('attachment', 'file');

.. caution::

    N'oubliez pas d'ajouter l'attribut ``enctype`` dans la balise form : 
	``<form action="#" method="post" {{ form_enctype(form) }}>``.

Lorsque le formulaire est soumis, le champ ``attachment`` sera une instance de
:class:`Symfony\\Component\\HttpFoundation\\File\\UploadedFile`. Elle peut �tre
utilis�e pour d�placer le fichier ``attachment`` vers son emplacement d�finitif :

.. code-block:: php

    use Symfony\Component\HttpFoundation\File\UploadedFile;

    public function uploadAction()
    {
        // ...

        if ($form->isValid()) {
            $someNewFilename = ...
        
            $form['attachment']->getData()->move($dir, $someNewFilename);

            // ...
        }

        // ...
    }

La m�thode ``move()`` prend un r�pertoire et un nom de fichier comme arguments.
Vous pouvez calculer le nom de fichier gr�ce � l'une des m�thodes suivantes::

    // utiliser le nom de fichier original
    $file->move($dir, $file->getClientOriginalName());

    // g�n�rer un nom al�atoire et essayer de deviner l'extension (plus s�curis�)
    $extension = $file->guessExtension();
    if (!$extension) {
        // l'extension n'a pas �t� trouv�e
        $extension = 'bin';
    }
    $file->move($dir, rand(1, 99999).'.'.$extension);

Utiliser le nom original via la m�thode ``getClientOriginalName()`` n'est pas s�curis�
car il a pu �tre manipul� par l'utilisateur. De plus, il peut contenir des caract�res
qui ne sont pas utilis�s dans les noms de fichiers. Il est recommand� de nettoyer
le nom avant de l'utiliser.

Lisez le chapitre :doc:`cookbook </cookbook/doctrine/file_uploads>` pour avoir un
exemple d'upload de fichier associ� � une entit� Doctrine.

Options h�rit�es
----------------

Ces options sont h�rit�es du type :doc:`field</reference/forms/types/field>` :

.. include:: /reference/forms/types/options/required.rst.inc

.. include:: /reference/forms/types/options/label.rst.inc

.. include:: /reference/forms/types/options/read_only.rst.inc

.. include:: /reference/forms/types/options/error_bubbling.rst.inc