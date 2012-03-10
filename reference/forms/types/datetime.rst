.. index::
   single: Forms; Fields; datetime

Type de champ Datetime
======================

Ce type de champ permet � l'utilisateur de manipuler une donn�e qui repr�sente
une date et une heure (ex: ``1984-06-05 12:15:30``).

Il peut �tre rendu comme un input text ou des balises select. Le format de la donn�e
r�elle peut �tre un objet ``DateTime``, une string, un timestamp ou un tableau.

+----------------------+-----------------------------------------------------------------------------+
| Type de donn�es      | peut �tre ``DateTime``, une chaine de caract�res, un timestamp,             |
|                      | ou un tableau (voir l'option ``input``)                                     |
+----------------------+-----------------------------------------------------------------------------+
| Rendu comme          | simple champ texte ou trois champs select                                   |
+----------------------+-----------------------------------------------------------------------------+
| Options              | - `date_widget`_                                                            |
|                      | - `time_widget`_                                                            |
|                      | - `input`_                                                                  |
|                      | - `date_format`_                                                            |
|                      | - `hours`_                                                                  |
|                      | - `minutes`_                                                                |
|                      | - `seconds`_                                                                |
|                      | - `years`_                                                                  |
|                      | - `months`_                                                                 |
|                      | - `days`_                                                                   |
|                      | - `with_seconds`_                                                           |
|                      | - `data_timezone`_                                                          |
|                      | - `user_timezone`_                                                          |
+----------------------+-----------------------------------------------------------------------------+
| Type parent          | :doc:`form</reference/forms/types/form>`                                    |
+----------------------+-----------------------------------------------------------------------------+
| Classe               | :class:`Symfony\\Component\\Form\\Extension\\Core\\Type\\DateTimeType`      |
+----------------------+-----------------------------------------------------------------------------+

Options du champ
----------------

date_widget
~~~~~~~~~~~

**type**: ``string`` **default**: ``choice``

D�finit l'option ``widget`` pour le type :doc:`date</reference/forms/types/date>`

time_widget
~~~~~~~~~~~

**type**: ``string`` **default**: ``choice``

D�finit l'option ``widget`` pour le type :doc:`time</reference/forms/types/time>`

input
~~~~~

**type**: ``string`` **default**: ``datetime``

Le format de la donn�e *finale* - c'est-�-dire le format sous lequel la date
est stock�e dans l'objet. Les valeurs valides sont :

* ``string`` (ex: ``2011-06-05 12:15:00``)
* ``datetime`` (un objet ``DateTime``)
* ``array`` (ex: ``array(2011, 06, 05, 12, 15, 0)``)
* ``timestamp`` (ex: ``1307276100``)

La valeur provenant du formulaire sera aussi normalis�e dans ce format.

date_format
~~~~~~~~~~~

**type**: ``integer`` ou ``string`` **default**: ``IntlDateFormatter::MEDIUM``

D�finit l'option ``format`` qui sera pass�e au champ date.

.. include:: /reference/forms/types/options/hours.rst.inc

.. include:: /reference/forms/types/options/minutes.rst.inc

.. include:: /reference/forms/types/options/seconds.rst.inc

.. include:: /reference/forms/types/options/years.rst.inc

.. include:: /reference/forms/types/options/months.rst.inc

.. include:: /reference/forms/types/options/days.rst.inc

.. include:: /reference/forms/types/options/with_seconds.rst.inc

.. include:: /reference/forms/types/options/data_timezone.rst.inc

.. include:: /reference/forms/types/options/user_timezone.rst.inc
