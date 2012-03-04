.. index::
   single: Forms; Fields; csrf

Type de champ Csrf
==================

Le type ``csrf`` est un champ input hidden qui contient le CSRF token (ou jeton).

+-------------+--------------------------------------------------------------------+
| Rendu comme | Champ ``input`` ``hidden``                                         |
+-------------+--------------------------------------------------------------------+
| Options     | - ``csrf_provider``                                                |
|             | - ``intention``                                                    |
|             | - ``property_path``                                                |
+-------------+--------------------------------------------------------------------+
| Type parent | ``hidden``                                                         |
+-------------+--------------------------------------------------------------------+
| Classe      | :class:`Symfony\\Component\\Form\\Extension\\Csrf\\Type\\CsrfType` |
+-------------+--------------------------------------------------------------------+

Options du champ
----------------

csrf_provider
~~~~~~~~~~~~~

**type**: ``Symfony\Component\Form\CsrfProvider\CsrfProviderInterface``

L'objet ``CsrfProviderInterface`` qui doit g�n�rer le CSRF token.
S'il n'est pas d�fini, la valeur par d�faut est le provider par d�faut.

intention
~~~~~~~~~

**type**: ``string``

Un identifiant unique facultatif pour g�n�rer le CSRF token.

.. include:: /reference/forms/types/options/property_path.rst.inc