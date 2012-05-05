.. index::
   single: Forms; Fields; repeated

Type de champ Repeated
======================

C'est un � groupe � sp�cial de champs qui cr�e deux champs identiques dont les valeurs
doivent correspondre (sinon une erreur de validation s'affiche). L'usage le plus commun
est lorsque vous avez besoin que l'utilisateur tape une nouvelle fois son mot de passe
ou son email pour v�rifier qu'ils sont justes.

+-------------+------------------------------------------------------------------------+
| Rendu comme | Champ input ``text`` par d�faut, mais voyez l'option `type`_ option    |
+-------------+------------------------------------------------------------------------+
| Options     | - `type`_                                                              |
|             | - `options`_                                                           |
|             | - `first_options`_                                                     |
|             | - `second_options`_                                                    |
|             | - `first_name`_                                                        |
|             | - `second_name`_                                                       |
+-------------+------------------------------------------------------------------------+
| Options     | - `invalid_message`_                                                   |
| h�rit�es    | - `invalid_message_parameters`_                                        |
|             | - `error_bubbling`_                                                    |
+-------------+------------------------------------------------------------------------+
| Type parent | :doc:`field</reference/forms/types/form>`                              |
+-------------+------------------------------------------------------------------------+
| Classe      | :class:`Symfony\\Component\\Form\\Extension\\Core\\Type\\RepeatedType` |
+-------------+------------------------------------------------------------------------+

Exemple d'utilisation
---------------------

.. code-block:: php

    $builder->add('password', 'repeated', array(
        'type' => 'password',
        'invalid_message' => 'Les mots de passe doivent correspondre',
        'options' => array('required' => true),
        'first_options'  => array('label' => 'Mot de passe'),
        'second_options' => array('label' => 'Mot de passe (validation)'),
    ));

Lors de la soumission r�ussie d'un formulaire, la valeur saisie dans les deux
champs � password � devient la donn�e de la cl� ``password``. En d'autres termes,
m�me si deux champs sont soumis en r�alit�, la donn�e finale du formulaire est juste
la valeur unique dont vous avez besoin (g�n�ralement une chaine de caract�res).

L'option la plus importante est ``type``, qui peut �tre n'importe quel type de champ
et qui d�termine le r�el type des deux champs sous-jacents. L'option ``options`` est pass�e
� chacun de ces deux champs ce qui signifie, dans cet exemple, que toute option
support�e par le type ``password`` peut �tre pass�e dans ce tableau.

Validation
~~~~~~~~~~

L'une des fonctionnalit�s cl� du champ ``repeated`` est sa validation interne
(vous n'avez rien besoin de faire pour l'activer) qui force les 2 champs � avoir
la m�me valeur. Si les deux valeurs ne sont pas identiques, une erreur sera
envoy�e � l'utilisateur.

L'option ``invalid_message`` est utilis�e pour personnaliser l'erreur qui
sera affich�e si les deux valeurs ne correspondent pas.

Field Options
-------------

type
~~~~

**type**: ``string`` **default**: ``text``

Les deux champs sous-jacents auront ce type de champ. Par exemple, passer le
type ``password`` retournera deux champs � mot de passe �.

options
~~~~~~~

**type**: ``array`` **default**: ``array()``

Ce tableau d'options sera pass� � chacun des deux champs sous-jacents. En d'autres
termes, ce sont les options qui personnalisent les types de champs individuellement.
Par exemple, si l'option ``type`` est d�finie comme ``password``, ce tableau peut
contenir les options ``always_empty`` ou ``required``, c'est-�-dire deux options qui
sont support�es par le type de champ ``password``.

first_options
~~~~~~~~~~~~~

**type**: ``array`` **default**: ``array()``

.. versionadded:: 2.1
    L'option ``first_options`` est une nouveaut� de Symfony 2.1.

Option additionnelle (elle sera fusionn�e avec `options` ci-dessus) qui devrait
�tre pass�e *uniquement* au premier champ. Elle est essentiellement utile pour
personnaliser le libell�::

    $builder->add('password', 'repeated', array(
        'first_options'  => array('label' => 'Mot de passe'),
        'second_options' => array('label' => 'Mot de passe (validation)'),
    ));

second_options
~~~~~~~~~~~~~~

**type**: ``array`` **default**: ``array()``

.. versionadded:: 2.1
    L'option ``second_options`` est une nouveaut� de Symfony 2.1.

Option additionnelle (elle sera fusionn�e avec `options` ci-dessus) qui devrait
�tre pass�e *uniquement* au premier champ. Elle est essentiellement utile pour
personnaliser le libell� (voir `first_options`_).

first_name
~~~~~~~~~~

**type**: ``string`` **default**: ``first``

C'est le nom de champ qui sera utilis� par le premier champ. Ce n'est en fait
pas tr�s important puisque la donn�e saisie dans les deux champs sera disponible
en utilisant la cl� du champ ``repeated`` lui-m�me (ex ``password``).
Cependant, si vous ne sp�cifiez pas de libell�, ce nom de champ est utilis� pour
deviner le libell� � votre place.

second_name
~~~~~~~~~~~

**type**: ``string`` **default**: ``second``

Le m�me que ``first_name``, mais pour le second champ.

Options h�rit�es
----------------

Ces options h�ritent du type :doc:`field</reference/forms/types/field>` :

.. include:: /reference/forms/types/options/invalid_message.rst.inc

.. include:: /reference/forms/types/options/invalid_message_parameters.rst.inc

.. include:: /reference/forms/types/options/error_bubbling.rst.inc
