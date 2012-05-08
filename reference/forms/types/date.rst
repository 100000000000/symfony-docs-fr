.. index::
   single: Forms; Fields; date

Type de champ Date
==================

Un champ qui permet � l'utilisateur de modifier une date via diff�rents �l�ments
HTML.

Les donn�es utilis�es par ce type de champ peuvent �tre un objet ``DateTime``,
une chaine de caract�res, un timestamp ou un tableau. Tant que l'option `input`_
est correctement d�finie, le champ s'occupera de tous les d�tails.

Le champ peut �tre rendu comme un simple champ texte, trois champs texte (mois,
jour et ann�e) ou comme trois listes d�roulantes (voyez l'option `widget_`).

+----------------------+-----------------------------------------------------------------------------+
| Type de donn�es      | peut �tre ``DateTime``, une chaine de caract�res, un timestamp, ou un       |
|                      | tableau (voir l'option ``input``)                                           |
+----------------------+-----------------------------------------------------------------------------+
| Rendu comme          | champ texte unique, trois champs textes, ou trois listes d�roulantes        |
+----------------------+-----------------------------------------------------------------------------+
| Options              | - `widget`_                                                                 |
|                      | - `input`_                                                                  |
|                      | - `empty_value`_                                                            |
|                      | - `years`_                                                                  |
|                      | - `months`_                                                                 |
|                      | - `days`_                                                                   |
|                      | - `format`_                                                                 |
|                      | - `pattern`_                                                                |
|                      | - `data_timezone`_                                                          |
|                      | - `user_timezone`_                                                          |
+----------------------+-----------------------------------------------------------------------------+
| Options              | - `invalid_message`_                                                        |
| h�rit�es             | - `invalid_message_parameters`_                                             |
+----------------------+-----------------------------------------------------------------------------+
| Type parent          | ``field`` (si texte), ``form`` sinon                                        |
+----------------------+-----------------------------------------------------------------------------+
| Classe               | :class:`Symfony\\Component\\Form\\Extension\\Core\\Type\\DateType`          |
+----------------------+-----------------------------------------------------------------------------+

Utilisation basique
-------------------

Ce type de champ est enti�rement configurable mais tr�s facile � utiliser. Les options
les plus importantes sont ``input`` et ``widget``.

Supposons que vous ayez un champ ``publishedAt`` dont la date est un objet ``DateTime``.
L'exemple suivant montre comment configurer le type ``date`` pour que le champ soit
rendu comme trois diff�rents champs Choice (listes d�roulantes) :

.. code-block:: php

    $builder->add('publishedAt', 'date', array(
        'input'  => 'datetime',
        'widget' => 'choice',
    ));

L'option ``input`` *doit* �tre chang�e pour correspondre au type de donn�e de la date.
Par exemple, si la donn�e du champ ``publishedAt`` est un timestamp unix, vous
aurez besoin de d�finir ``input`` � ``timestamp``:

.. code-block:: php

    $builder->add('publishedAt', 'date', array(
        'input'  => 'timestamp',
        'widget' => 'choice',
    ));

Le champ supporte aussi un ``array`` ou une ``string`` comme valeurs valides de
l'option ``input``.

Options du champ
----------------

.. include:: /reference/forms/types/options/date_widget.rst.inc

.. _form-reference-date-input:

.. include:: /reference/forms/types/options/date_input.rst.inc

empty_value
~~~~~~~~~~~

**type**: ``string`` ou ``array``

Si votre option Widget est d�finie � ``choice``, alors ce champ sera repr�sent� comme
une s�rie de listes d�roulantes (``select``). L'option ``empty_value`` peut �tre
utilis�e pour d�finir un choix � vide � en haut de chaque liste d�roulante::

    $builder->add('dueDate', 'date', array(
        'empty_value' => '',
    ));

Sinon, vous pouvez aussi sp�cifier une chaine de caract�res qui sera affich�e pour
la valeur � vide�::

    $builder->add('dueDate', 'date', array(
        'empty_value' => array('year' => 'Year', 'month' => 'Month', 'day' => 'Day')
    ));

.. include:: /reference/forms/types/options/years.rst.inc

.. include:: /reference/forms/types/options/months.rst.inc

.. include:: /reference/forms/types/options/days.rst.inc

.. _reference-forms-type-date-format:

.. include:: /reference/forms/types/options/date_format.rst.inc

.. include:: /reference/forms/types/options/date_pattern.rst.inc

.. include:: /reference/forms/types/options/data_timezone.rst.inc

.. include:: /reference/forms/types/options/user_timezone.rst.inc

Options h�rit�es
----------------

Ces options h�ritent du type :doc:`field</reference/forms/types/field>` :

.. include:: /reference/forms/types/options/invalid_message.rst.inc

.. include:: /reference/forms/types/options/invalid_message_parameters.rst.inc
