.. index::
   single: Forms; Fields; integer

Type de champ Integer
=====================

Affiche un champ input � number �. De fa�on basique, c'est un champ texte qui sait bien 
g�rer les donn�es enti�res d'un formulaire. Le champ input ``number`` ressemble �
un champ texte, except� que, si le navigateur supporte l'HTML5, il aura des fonctionnalit�s
suppl�mentaires.

Ce champ a diff�rentes options permettant de d�finir comment g�rer les valeurs qui
ne sont pas des entiers. Par d�faut, toutes les valeurs non enti�res (ex: 6,78)
seront arrondies � l'entier inf�rieur (ex: 6).

+-------------+-----------------------------------------------------------------------+
| Rendu comme | Champ ``input`` ``text``                                              |
+-------------+-----------------------------------------------------------------------+
| Options     | - `rounding_mode`_                                                    |
|             | - `grouping`_                                                         |
+-------------+-----------------------------------------------------------------------+
| Options     | - `required`_                                                         |
| h�rit�es    | - `label`_                                                            |
|             | - `read_only`_                                                        |
|             | - `error_bubbling`_                                                   |
+-------------+-----------------------------------------------------------------------+
| Type parent | :doc:`field</reference/forms/types/field>`                            |
+-------------+-----------------------------------------------------------------------+
| Classe      | :class:`Symfony\\Component\\Form\\Extension\\Core\\Type\\IntegerType` |
+-------------+-----------------------------------------------------------------------+

Options du champ
----------------

rounding_mode
~~~~~~~~~~~~~

**type**: ``integer`` **default**: ``IntegerToLocalizedStringTransformer::ROUND_DOWN``

Par d�faut, si l'utilisateur entre un nombre qui n'est pas entier, il sera arrondi
� l'entier inf�rieur. Il y a plusieurs autres m�thodes pour arrondir, et chacune
est une constante de la classe :class:`Symfony\\Component\\Form\\Extension\\Core\\DataTransformer\\IntegerToLocalizedStringTransformer`:

*   ``IntegerToLocalizedStringTransformer::ROUND_DOWN`` Mode pour arrondir jusqu'� z�ro.

*   ``IntegerToLocalizedStringTransformer::ROUND_FLOOR`` Mode pour arrondir jusqu'�
    l'infini n�gatif.

*   ``IntegerToLocalizedStringTransformer::ROUND_UP`` Mode pour arrondir en partant
    de z�ro.

*   ``IntegerToLocalizedStringTransformer::ROUND_CEILING`` Mode pour arrondir jusqu'�
    l'infini positif.

.. include:: /reference/forms/types/options/grouping.rst.inc

Options h�rit�es
----------------

Ces options h�ritent du type :doc:`field</reference/forms/types/field>` :

.. include:: /reference/forms/types/options/required.rst.inc

.. include:: /reference/forms/types/options/label.rst.inc

.. include:: /reference/forms/types/options/read_only.rst.inc

.. include:: /reference/forms/types/options/error_bubbling.rst.inc
