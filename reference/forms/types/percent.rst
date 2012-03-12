.. index::
   single: Forms; Fields; percent

Type de champ Percent
=====================

Le type ``percent`` rend un champ input texte sp�cialis� dans la gestion de pourcentages.
Si votre pourcentage est stock� comme d�cimale (ex ``0,95``),
vous pouvez utiliser ce champ directement. Si vous stockez votre donn�es comme nombre
(ex ``95``), vous devriez d�finir l'option ``type`` � ``integer``.

Ce champ ajoute le signe pourcentage "``%``" apr�s l'input.

+-------------+-----------------------------------------------------------------------+
| Rendu comme | Champ ``input`` ``text``                                              |
+-------------+-----------------------------------------------------------------------+
| Options     | - `type`_                                                             |
|             | - `precision`_                                                        |
+-------------+-----------------------------------------------------------------------+
| Options     | - `required`_                                                         |
| h�rit�es    | - `label`_                                                            |
|             | - `read_only`_                                                        |
|             | - `error_bubbling`_                                                   |
+-------------+-----------------------------------------------------------------------+
| Type parent | :doc:`field</reference/forms/types/field>`                            |
+-------------+-----------------------------------------------------------------------+
| Classe      | :class:`Symfony\\Component\\Form\\Extension\\Core\\Type\\PercentType` |
+-------------+-----------------------------------------------------------------------+

Options
-------

type
~~~~

**type**: ``string`` **default**: ``fractional``

Cette option contr�le la fa�on dont vos donn�es sont stock�es dans l'objet. Par exemple,
un pourcentage correspondant � � 55% �, peut �tre stock� comme ``0,55`` ou ``55`` dans votre
objet. Les deux � types � g�rent ces deux cas :
    
*   ``fractional``
    Si votre donn�e est stock�e au format d�cimal (ex ``0,55``), utilisez ce type.
    La donn�e sera multipli�e par ``100`` avant d'�tre affich�e � l'utilisateur (ex ``55``).
	La valeur soumise sera divis�e par ``100`` lors de la soumission du formulaire pour que
	la valeur soit stock�e au format d�cimal (``0,55``);

*   ``integer``
    Si votre donn�e est stock�e comme integer (ex 55), utilisez cette
	option. La valeur brute (``55``) est affich�e � l'utilisateur et stock�e dans votre objet.
	Notez que cela ne fonctionne que pour les valeurs enti�res.

precision
~~~~~~~~~

**type**: ``integer`` **default**: ``0``

Par d�faut, les nombres sont arrondis. Pour autoriser les d�cimales, utilisez cette option.

Options h�rit�es
----------------

Ces options h�ritent du type :doc:`field</reference/forms/types/field>` :

.. include:: /reference/forms/types/options/required.rst.inc

.. include:: /reference/forms/types/options/label.rst.inc

.. include:: /reference/forms/types/options/read_only.rst.inc

.. include:: /reference/forms/types/options/error_bubbling.rst.inc

