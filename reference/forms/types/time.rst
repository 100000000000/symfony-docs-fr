.. index::
   single: Forms; Fields; time

Type de champ Time
==================

Un champ pour saisir un temps.

Ce champ peut �tre affich� comme champ texte, une s�rie de champs texte (ex heures, minutes,
secondes) ou une s�rie de listes d�roulantes. La donn�e finale peut �tre stock�e comme un objet
``DateTime``, une chaine de caract�res, un timestamp ou un tableau.

+----------------------+-----------------------------------------------------------------------------+
| Type de donn�e       | Peut �tre un objet``DateTime``, une chaine de caract�re, un timestamp,      |
|                      | ou un tableau (voir l'option ``input`` )                                    |
+----------------------+-----------------------------------------------------------------------------+
| Rendu comme          | peut �tre diff�rentes balises (voir plus bas)                               |
+----------------------+-----------------------------------------------------------------------------+
| Options              | - `widget`_                                                                 |
|                      | - `input`_                                                                  |
|                      | - `with_seconds`_                                                           |
|                      | - `hours`_                                                                  |
|                      | - `minutes`_                                                                |
|                      | - `seconds`_                                                                |
|                      | - `data_timezone`_                                                          |
|                      | - `user_timezone`_                                                          |
+----------------------+-----------------------------------------------------------------------------+
| Options              | - `invalid_message`_                                                        |
| h�rit�es             | - `invalid_message_parameters`_                                             |
+----------------------+-----------------------------------------------------------------------------+
| Type parent          | form                                                                        |
+----------------------+-----------------------------------------------------------------------------+
| Classe               | :class:`Symfony\\Component\\Form\\Extension\\Core\\Type\\TimeType`          |
+----------------------+-----------------------------------------------------------------------------+

Utilisation basique
-------------------

Ce type de champ est enti�rement configurable mais tr�s facile � utiliser. Les options
les plus importantes sont ``input`` et ``widget``.

Supposez que vous avec un champ ``startTime`` dont la donn�e sous-jacente est un objet
``DateTime``. L'exemple suivant configure le type ``time`` pour que le champ soit compos�
de trois listes d�roulantes :

.. code-block:: php

    $builder->add('startTime', 'time', array(
        'input'  => 'datetime',
        'widget' => 'choice',
    ));

L'option ``input`` *doit* �tre chang�e pour correspondre au type de donn�e date sous-jacent.
Par exemple, si la donn�es du champ ``startTime`` est un timestamp unix, vous devrez d�finir
l'option ``input`` � ``timestamp`` :

.. code-block:: php

    $builder->add('startTime', 'time', array(
        'input'  => 'timestamp',
        'widget' => 'choice',
    ));

Le champ supporte aussi ``array`` et ``string`` comme valeurs valides de l'option ``input``.

Options du champ
----------------

widget
~~~~~~

**type**: ``string`` **default**: ``choice``


Cette option d�finit la mani�re dont le champ doit �tre affich�. Les choix suivants sont possibles :

* ``choice``: rend deux (ou trois si `with_seconds`_ est � true) listes d�roulantes.

* ``text``: rend deux ou trois champs input texte (heures, minutes, secondes).

* ``single_text``: rend un simple input texte. La donn�e saisie sera valid�e en fonction
  du format ``hh:mm`` (ou ``hh:mm:ss`` si vous utilisez les secondes).

input
~~~~~

**type**: ``string`` **default**: ``datetime``

Le format de la donn�e *finale*, c'est-�-dire le format dans lequel la donn�e
sera stock�e dans votre objet. Les valeurs autoris�es sont :

* ``string`` (ex ``12:17:26``)
* ``datetime`` (un objet``DateTime``)
* ``array`` (ex ``array('hour' => 12, 'minute' => 17, 'second' => 26)``)
* ``timestamp`` (ex ``1307232000``)

la valeur qui provient du formulaire sera �galement normalis�e selon ce format.

.. include:: /reference/forms/types/options/with_seconds.rst.inc

.. include:: /reference/forms/types/options/hours.rst.inc

.. include:: /reference/forms/types/options/minutes.rst.inc

.. include:: /reference/forms/types/options/seconds.rst.inc

.. include:: /reference/forms/types/options/data_timezone.rst.inc

.. include:: /reference/forms/types/options/user_timezone.rst.inc

Options h�rit�es
----------------

Ces options h�ritent du type :doc:`field</reference/forms/types/field>` :

.. include:: /reference/forms/types/options/invalid_message.rst.inc

.. include:: /reference/forms/types/options/invalid_message_parameters.rst.inc
