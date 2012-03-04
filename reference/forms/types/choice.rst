.. index::
   single: Forms; Fields; choice

Type de champ Choice
====================

Un champ multi-usage pour permettre � l'utilisateur de "choisir" une ou plusieurs
options. Il peut �tre affich� avec des balises ``select``, des boutons radio, ou
des checkboxes.

Pour utiliser ce champ, vous devez sp�cifier *soit l'option* ``choice_list``, *soit* ``choices``.

+-------------+-----------------------------------------------------------------------------+
| Rendu comme | peut �tre diff�rentes balises (voir ci-dessous)                             |
+-------------+-----------------------------------------------------------------------------+
| Options     | - `choices`_                                                                |
|             | - `choice_list`_                                                            |
|             | - `multiple`_                                                               |
|             | - `expanded`_                                                               |
|             | - `preferred_choices`_                                                      |
|             | - `empty_value`_                                                            |
|             | - `empty_data`_                                                             |
+-------------+-----------------------------------------------------------------------------+
| Options     | - `required`_                                                               |
| h�rit�es    | - `label`_                                                                  |
|             | - `read_only`_                                                              |
|             | - `error_bubbling`_                                                         |
+-------------+-----------------------------------------------------------------------------+
| Type parent | :doc:`form</reference/forms/types/form>` (if expanded), ``field`` otherwise |
+-------------+-----------------------------------------------------------------------------+
| Classe      | :class:`Symfony\\Component\\Form\\Extension\\Core\\Type\\ChoiceType`        |
+-------------+-----------------------------------------------------------------------------+

Exemple d'utilisation
---------------------

La mani�re la plus facile d'utiliser ce champ est de sp�cifier directement les
choix possibles via l'option ``choices``. L'index du tableau deviendra la valeur
qui sera effectivement d�finie dans votre objet final (ex: ``m``), alors que la valeur
est ce que verra l'utilisateur dans le formulaire (ex: ``Masculin``).

.. code-block:: php

    $builder->add('gender', 'choice', array(
        'choices'   => array('m' => 'Masculin', 'f' => 'F�minin'),
        'required'  => false,
    ));

En d�finissant l'option ``multiple`` � true, vous pouvez autoriser l'utilisateur � 
choisir plusieurs valeurs. Le widget sera rendu comme une balide``select`` multiple, ou
comme une s�rie de checkboxes en fonction de l'option ``expanded`` :

.. code-block:: php

    $builder->add('availability', 'choice', array(
        'choices'   => array(
            'matin'   => 'Matin',
            'apresmidi' => 'Apr�s-midi',
            'soir'   => 'Soir',
        ),
        'multiple'  => true,
    ));

Vous pouvez aussi utiliser l'option ``choice_list``, qui prend un objet comme argument
pour sp�cifier les choix de votre widget.

.. _forms-reference-choice-tags:

.. include:: /reference/forms/types/options/select_how_rendered.rst.inc

Options du champ
----------------

choices
~~~~~~~

**type**: ``array`` **default**: ``array()``

C'est la fa�on la plus simple de sp�cifier les choix qui pourront �tre choisis 
dans le champ. L'option ``choices`` est un tableay, o� les index sont les valeurs
des items, et les valeurs du tableau sont les labels des items :

.. code-block:: php

    $builder->add('gender', 'choice', array(
        'choices' => array('m' => 'Masculin', 'f' => 'F�minin')
    ));

choice_list
~~~~~~~~~~~

**type**: ``Symfony\Component\Form\Extension\Core\ChoiceList\ChoiceListInterface``

C'est une fa�on de sp�cifier les options de champ � utiliser. L'option ``choice_list``
doit �tre une instance de ``ChoiceListInterface``.
Pour des cas plus avanc�s, une classe personnalis�e qui impl�mente l'interface peut
�tre cr��e pour d�finir les choix.

.. include:: /reference/forms/types/options/multiple.rst.inc

.. include:: /reference/forms/types/options/expanded.rst.inc

.. include:: /reference/forms/types/options/preferred_choices.rst.inc

.. include:: /reference/forms/types/options/empty_value.rst.inc

.. include:: /reference/forms/types/options/empty_data.rst.inc

Options h�rit�es
----------------

Ces options h�ritent du type :doc:`field</reference/forms/types/field>` :

.. include:: /reference/forms/types/options/required.rst.inc

.. include:: /reference/forms/types/options/label.rst.inc

.. include:: /reference/forms/types/options/read_only.rst.inc

.. include:: /reference/forms/types/options/error_bubbling.rst.inc
