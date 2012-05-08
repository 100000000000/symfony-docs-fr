.. index::
   single: Forms; Fields; money

Type de champ Money
===================

Rend un champ input texte sp�cialis� dans la gestion des donn�es mon�taires.

Ce type de champ vous permet de sp�cifier une devise, dont le symbole sera affich�
� c�t� du champ texte. Il y a plusieurs autres options pour personnaliser la fa�on
dont les donn�es en entr�e et en sortie seront prises en charge.

+-------------+---------------------------------------------------------------------+
| Rendu comme | Champ ``input`` ``text``                                            |
+-------------+---------------------------------------------------------------------+
| Options     | - `currency`_                                                       |
|             | - `divisor`_                                                        |
|             | - `precision`_                                                      |
|             | - `grouping`_                                                       |
+-------------+---------------------------------------------------------------------+
| Options     | - `required`_                                                       |
| h�rit�es    | - `label`_                                                          |
|             | - `read_only`_                                                      |
|             | - `error_bubbling`_                                                 |
|             | - `invalid_message`_                                                |
|             | - `invalid_message_parameters`_                                     |
+-------------+---------------------------------------------------------------------+
| Type parent | :doc:`field</reference/forms/types/field>`                          |
+-------------+---------------------------------------------------------------------+
| Classe      | :class:`Symfony\\Component\\Form\\Extension\\Core\\Type\\MoneyType` |
+-------------+---------------------------------------------------------------------+

Options du champ
----------------

currency
~~~~~~~~

**type**: ``string`` **default**: ``EUR``

D�finit la devise dans laquelle la somme est sp�cifi�e. Cela d�termine quel symbole
mon�taire sera affich� dans le champ texte. Selon la devise choisie, le symbole
s'affichera avant ou apr�s la donn�e dans le champ texte.

Cette option peut aussi �tre d�finie � false pour cacher le symbole mon�taire.

divisor
~~~~~~~

**type**: ``integer`` **default**: ``1``

Si, pour une raison quelconque, vous avez besoin de diviser votre valeur de d�part par un
nombre avant de le rendre � l'utilisateur, vous pouvez utiliser l'option ``divisor``.
Par exemple::

    $builder->add('price', 'money', array(
        'divisor' => 100,
    ));

Dans ce cas, si le champ ``price`` est d�fini � ``9900``, alors c'est en fait la valeur
``99`` qui sera affich�e � l'utilisateur. Lorsque l'utilisateur soumettra la valeur
``99``, elle sera automatiquement multipli�e par ``100`` et ``9900`` sera la valeur
finalement stock�e dans votre projet.

precision
~~~~~~~~~

**type**: ``integer`` **default**: ``2``

Si pour une raison quelconque vous avez besoin d'une autre pr�cision que 2 d�cimales,
vous pouvez modifier cette option. Vous n'aurez probablement pas besoin de le faire
� moins, par exemple, que vous ne vouliez arrondir au dollar le plus proche (dans
ce cas, d�finissez la pr�cision � ``0``).

.. include:: /reference/forms/types/options/grouping.rst.inc

Options h�rit�es
----------------

Ces options h�ritent du type :doc:`field</reference/forms/types/field>` :

.. include:: /reference/forms/types/options/required.rst.inc

.. include:: /reference/forms/types/options/label.rst.inc

.. include:: /reference/forms/types/options/read_only.rst.inc

.. include:: /reference/forms/types/options/error_bubbling.rst.inc

.. include:: /reference/forms/types/options/invalid_message.rst.inc

.. include:: /reference/forms/types/options/invalid_message_parameters.rst.inc
