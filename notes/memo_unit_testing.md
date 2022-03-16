# Test unitaire

dernière mise à jour : 15/03/2022

## PHP et PHPUnit
phpUnit librairie de référence pour le test unitaire. 

## Objectifs

Ecriture de tests automatisés pour : 
  * Feedback rapide
  * Maintenabilité
  * Protection contre la régression
  * Résistance au refactoring
 
 ## Concepts
 
 ### Taux de couverture du code 
 
 Un indicateur basé sur la formule simple : 
 
 `Couverture de test = Nb Lignes Executées (code) / Total de lignes (tu)`
 
 Un indicateur peu fiable, qui ne présume pas de la qualité des tests et des cas testés.
 
 ### Définition d'une suite de tests efficace
 
 * Intégrée au cycle de développement, donc exécutée à chaque modification de code.
 * Cible les parties les plus importantes du code.
 * Produit un maximum de valeur pour un minimum de coût de maintenance.

### Mock et doublure de test

Le **mock** fournit une doublure de test, qui permet de substituer un objet dont la classe à tester (ou SUT) est dépendante.
Nous pouvons coder son comportement et rendre ses sorties prédictibles. 

### Les dépendances de test
Elles sont de différentes natures : 
* API (située hors de l'application)
* Base de données
* FileSystem
* etc.

Ces dépendances nécessitent une setup et une configuration en prérequis de l'exécution des tests.
Elles peuvent êtres substitués ce qui apporte du confort (ex: vitesse d'exécution des tests).

### Granularité des tests 

Deux écoles existent : école classique VS école de Londres, que l'on peut résumer par :  
* définition du terme "Unitaire" (unit), est-il constitué par une classe ou un set de classes ? 

L'idée est de tester un **comportement** qui a du sens pour le domaine, idéalement identifiable comme utile pour une personne du métier.

