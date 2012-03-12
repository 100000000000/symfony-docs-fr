.. index::
   single: Forms; Fields; url

Type de champ Url
=================

Le champ ``url`` est un champ texte qui pr�fixe la valeur soumise par un protocole
donn� (ex ``http://``) si la valeur n'a pas d�j� un protocole.

+-------------+-------------------------------------------------------------------+
| Rendu comme | Champ ``input url``                                               |
+-------------+-------------------------------------------------------------------+
| Options     | - `default_protocol`_                                             |
+-------------+-------------------------------------------------------------------+
| Options     | - `max_length`_                                                   |
| h�rit�es    | - `required`_                                                     |
|             | - `label`_                                                        |
|             | - `trim`_                                                         |
|             | - `read_only`_                                                    |
|             | - `error_bubbling`_                                               |
+-------------+-------------------------------------------------------------------+
| Type parent | :doc:`text</reference/forms/types/text>`                          |
+-------------+-------------------------------------------------------------------+
| Classe      | :class:`Symfony\\Component\\Form\\Extension\\Core\\Type\\UrlType` |
+-------------+-------------------------------------------------------------------+

Options du champ
----------------

default_protocol
~~~~~~~~~~~~~~~~

**type**: ``string`` **default**: ``http``

Si une valeur soumise ne commence pas un protocole (ex ``http://``,
``ftp://``, etc), ce protocole sera ajout� au d�but de la chaine de caract�res
lorsque les donn�es seront associ�es au formulaire.

Options h�rit�es
----------------

Ces options h�ritent du type :doc:`field</reference/forms/types/field>` :

.. include:: /reference/forms/types/options/max_length.rst.inc

.. include:: /reference/forms/types/options/required.rst.inc

.. include:: /reference/forms/types/options/label.rst.inc

.. include:: /reference/forms/types/options/trim.rst.inc

.. include:: /reference/forms/types/options/read_only.rst.inc

.. include:: /reference/forms/types/options/error_bubbling.rst.inc
