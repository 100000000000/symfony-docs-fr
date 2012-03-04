.. index::
   single: Forms; Fields; checkbox

Type de champ Checkbox
======================

Cr�e un unique champ de type input checkbox. Cela devrait toujours �te utilis� pour
un champ qui a une valeur bool�enne : si la checkbox est coch�e, le champ sera
d�fini � true. Si la checkbox n'est pas coch�e, le champ sera d�fini � false.

+-------------+------------------------------------------------------------------------+
| Rendu comme | Champ ``input`` ``text``                                               |
+-------------+------------------------------------------------------------------------+
| Options     | - `value`_                                                             |
+-------------+------------------------------------------------------------------------+
| Options     | - `required`_                                                          |
| h�rit�es    | - `label`_                                                             |
|             | - `read_only`_                                                         |
|             | - `error_bubbling`_                                                    |
+-------------+------------------------------------------------------------------------+
| Type parent | :doc:`field</reference/forms/types/field>`                             |
+-------------+------------------------------------------------------------------------+
| Classe      | :class:`Symfony\\Component\\Form\\Extension\\Core\\Type\\CheckboxType` |
+-------------+------------------------------------------------------------------------+

Exemple d'utilisation
---------------------

.. code-block:: php

    $builder->add('public', 'checkbox', array(
        'label'     => 'Afficher publiquement ?',
        'required'  => false,
    ));

Options du champ
----------------

value
~~~~~

**type**: ``mixed`` **default**: ``1``

La valeur qui est effectivement utilis�e comme valeur de la checkbox. Cela n'affecte
pas la valeur qui est d�finie sur votre objet.

Options h�rit�es
----------------

Ces options h�ritent du type :doc:`field</reference/forms/types/field>` :

.. include:: /reference/forms/types/options/required.rst.inc

.. include:: /reference/forms/types/options/label.rst.inc

.. include:: /reference/forms/types/options/read_only.rst.inc

.. include:: /reference/forms/types/options/error_bubbling.rst.inc
