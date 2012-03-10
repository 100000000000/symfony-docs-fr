.. index::
   single: Forms; Fields; radio

Type de champ Radio
===================

Cr�e un simple bouton radio. Il devrait toujours �tre utilis� pour un champ
dont la valeur est bool�enne. : si le bouton radio est s�lectionn�, le champ sera
d�fini � true, sinon, la valeur sera d�finie � false.

Le type ``radio`` n'est g�n�ralement pas utilis� directement. Le plus souvent, il 
est utilis� indirectement par d'autres types comme le type :doc:`Choice</reference/forms/types/choice>`.
Si vous voulez avoir un champ Bool�en, utilisez :doc:`checkbox</reference/forms/types/checkbox>`.

+-------------+---------------------------------------------------------------------+
| Rendu comme | Champ ``input`` ``radio``                                           | 
+-------------+---------------------------------------------------------------------+
| Options     | - `value`_                                                          |
+-------------+---------------------------------------------------------------------+
| Options     | - `required`_                                                       |
| h�rit�es    | - `label`_                                                          |
|             | - `read_only`_                                                      |
|             | - `error_bubbling`_                                                 |
+-------------+---------------------------------------------------------------------+
| Type parent | :doc:`field</reference/forms/types/field>`                          |
+-------------+---------------------------------------------------------------------+
| Classe      | :class:`Symfony\\Component\\Form\\Extension\\Core\\Type\\RadioType` |
+-------------+---------------------------------------------------------------------+

Options du champ
----------------

value
~~~~~

**type**: ``mixed`` **default**: ``1``

La valeur qui est effectivement utilis�e comme valeur pour le radio bouton. Cela
n'affecte pas la valeur qui est d�finie dans votre objet.

Options h�rit�es
-----------------

Ces options h�ritent du type :doc:`field</reference/forms/types/field>` :

.. include:: /reference/forms/types/options/required.rst.inc

.. include:: /reference/forms/types/options/label.rst.inc

.. include:: /reference/forms/types/options/read_only.rst.inc

.. include:: /reference/forms/types/options/error_bubbling.rst.inc
