Contraintes de validation de r�f�rence
======================================

.. toctree::
   :maxdepth: 1
   :hidden:

   constraints/NotBlank
   constraints/Blank
   constraints/NotNull
   constraints/Null
   constraints/True
   constraints/False
   constraints/Type

   constraints/Email
   constraints/MinLength
   constraints/MaxLength
   constraints/Url
   constraints/Regex
   constraints/Ip

   constraints/Max
   constraints/Min

   constraints/Date
   constraints/DateTime
   constraints/Time

   constraints/Choice
   constraints/Collection
   constraints/UniqueEntity
   constraints/Language
   constraints/Locale
   constraints/Country

   constraints/File
   constraints/Image

   constraints/Callback
   constraints/All
   constraints/UserPassword
   constraints/Valid

Le Validator est con�u pour valider les objets selon des *contraintes*.
Dans la vie r�elle, une contrainte pourrait �tre : � Le g�teau ne doit
pas �tre br�l� �. Dans Symfony2, les contraintes sont similaires : ce sont
des assertions qu'une condition est v�rifi�e.

Contraintes support�es
----------------------

Les contraintes suivantes sont nativement support�es par Symfony2 :

.. include:: /reference/constraints/map.rst.inc
