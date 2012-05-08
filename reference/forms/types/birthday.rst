.. index::
   single: Forms; Fields; birthday

Type de champ Birthday
======================

Un champ :doc:`date</reference/forms/types/date>` qui est sp�cialis� dans la gestion
des dates de naissance.

Peut �tre rendu comme un champ texte unique, trois champs textes (mois, jour et ann�e),
ou trois listes d�roulantesS.

Ce type est tr�s similaire au type :doc:`date</reference/forms/types/date>`, mais
avec des valeurs par d�faut de l'option `years`_ plus appropri�es. L'option `years`_
contient par d�faut les 120 ann�es pr�c�dant l'ann�e courante.

+----------------------+------------------------------------------------------------------------------------------------------------------------+
| Type de donn�es      | peut �tre ``DateTime``, ``string``, ``timestamp``, ou ``array`` (voir :ref:`option input <form-reference-date-input>`) |
+----------------------+------------------------------------------------------------------------------------------------------------------------+
| Rendu comme          | soit trois select, soit 1 ou 3 champs texte, bas� sur l'option `widget`_                                               |
+----------------------+------------------------------------------------------------------------------------------------------------------------+
| Options              | - `years`_                                                                                                             |
+----------------------+------------------------------------------------------------------------------------------------------------------------+
| Options              | - `widget`_                                                                                                            |
| h�rit�es             | - `input`_                                                                                                             |
|                      | - `months`_                                                                                                            |
|                      | - `days`_                                                                                                              |
|                      | - `format`_                                                                                                            |
|                      | - `pattern`_                                                                                                           |
|                      | - `data_timezone`_                                                                                                     |
|                      | - `user_timezone`_                                                                                                     |
|                      | - `invalid_message`_                                                                                                   |
|                      | - `invalid_message_parameters`_                                                                                        |
+----------------------+------------------------------------------------------------------------------------------------------------------------+
| Type parent          | :doc:`date</reference/forms/types/date>`                                                                               |
+----------------------+------------------------------------------------------------------------------------------------------------------------+
| Classe               | :class:`Symfony\\Component\\Form\\Extension\\Core\\Type\\BirthdayType`                                                 |
+----------------------+------------------------------------------------------------------------------------------------------------------------+

Options du champ
----------------

years
~~~~~

**type**: ``array`` **default**: 120 ann�es pr�c�dant l'ann�e courante

Liste des ann�es disponibles pour le type de champ 'year'. Cette option n'est 
utile que si l'option ``widget`` est d�finie � ``choice``.

Options h�rit�es
----------------

Ces options h�ritent du type :doc:`date</reference/forms/types/date>` :

.. include:: /reference/forms/types/options/date_widget.rst.inc
    
.. include:: /reference/forms/types/options/date_input.rst.inc

.. include:: /reference/forms/types/options/months.rst.inc

.. include:: /reference/forms/types/options/days.rst.inc

.. include:: /reference/forms/types/options/date_format.rst.inc
    
.. include:: /reference/forms/types/options/date_pattern.rst.inc

.. include:: /reference/forms/types/options/data_timezone.rst.inc

.. include:: /reference/forms/types/options/user_timezone.rst.inc

Ces options h�ritent du type :doc:`date</reference/forms/types/field>` :

.. include:: /reference/forms/types/options/invalid_message.rst.inc

.. include:: /reference/forms/types/options/invalid_message_parameters.rst.inc
