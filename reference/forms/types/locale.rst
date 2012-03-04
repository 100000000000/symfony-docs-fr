.. index::
   single: Forms; Fields; locale

Type de champ Locale
====================

Le type ``locale`` est un sous-ensemble de ``ChoiceType`` qui permet � l'utilisateur
de choisir une locale (langue+pays) dans une liste d�roulante. En bonus, les noms des
locales sont affich�s dans la langue de l'utilisateur.


La "valeur" de chaque locale est soit le code *langue* ISO639-1 en deux lettres
(ex ``fr``), soit le code langue suivi d'un underscore  (``_``), puis le code
*pays* ISO3166 (ex ``fr_FR`` pour Fran�ais/France).

.. note::

   La locale de votre utilisateur est devin�e en utilisant `Locale::getDefault()`_

Contrairement au type ``choice``, vous n'avez pas besoin de sp�cifier les options
``choices`` ou ``choice_list`` puisque ce type de champ utilise automatiquement
la liste des locales. Vous *pouvez* sp�cifier l'une ou l'autre de ces options manuellement,
mais alors vous devriez plut�t utiliser directement le type ``choice``.

+-------------+------------------------------------------------------------------------+
| Rendered as | Peut �tre diff�rentes balises (voir :ref:`forms-reference-choice-tags`)|
+-------------+------------------------------------------------------------------------+
| Options     | - `multiple`_                                                          |
| h�rit�es    | - `expanded`_                                                          |
|             | - `preferred_choices`_                                                 |
|             | - `empty_value`_                                                       |
|             | - `error_bubbling`_                                                    |
|             | - `required`_                                                          |
|             | - `label`_                                                             |
|             | - `read_only`_                                                         |
+-------------+------------------------------------------------------------------------+
| Type parent | :doc:`choice</reference/forms/types/choice>`                           |
+-------------+------------------------------------------------------------------------+
| Classe      | :class:`Symfony\\Component\\Form\\Extension\\Core\\Type\\LanguageType` |
+-------------+------------------------------------------------------------------------+

Options h�rit�es
----------------

Ces options sont h�rit�es du type :doc:`choice</reference/forms/types/choice>` :

.. include:: /reference/forms/types/options/multiple.rst.inc

.. include:: /reference/forms/types/options/expanded.rst.inc

.. include:: /reference/forms/types/options/preferred_choices.rst.inc

.. include:: /reference/forms/types/options/empty_value.rst.inc

.. include:: /reference/forms/types/options/error_bubbling.rst.inc

Ces options sont h�rit�es du type :doc:`field</reference/forms/types/field>` :

.. include:: /reference/forms/types/options/required.rst.inc

.. include:: /reference/forms/types/options/label.rst.inc

.. include:: /reference/forms/types/options/read_only.rst.inc

.. _`Locale::getDefault()`: http://php.net/manual/en/locale.getdefault.php
