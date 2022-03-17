# Test unitaire

dernière mise à jour : 15/03/2022

## PHP et PHPUnit
phpUnit: librairie de référence pour le test unitaire en PHP.

## Tests sous Symfony 

Symfony introduit des composants de plus haut niveau, au dessus de PHPUnit, ex: 
* class `WebTestCase`  
* class `KernelTestCase`

Des commandes permettent de générer une BDD de tests ou encore, de générer automatiquement la structure des classes de tests (voir documentation Symfony).

## Objectifs

Ecriture de tests automatisés pour : 
  * **Feedback rapide**
  * **Maintenabilité**
  * **Protection contre la régression**
  * **Résistance au refactoring**
 
 ## Catégories de tests
 
 * **Test unitaire**: s'assurer qu'une partie individuel du code se comporte comme prévue (ex: Une classe, une méthode).
 * **Test d'intégration**: Tester une combinaison de colasse qui interéagisse entre elles (avec le service container par ex. sur Symfony).
 * **Test application**: Tester le comportement d'une application complète. Il s'agit de faire une requête HTTP (réel ou simulé via un Crawler),
 * et tester la réponse attendue. 
 
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

#### Méthodes de création de Mocks spécifique à PHPUnit
* `createMock`
* `getMockBuilder` (personnalisation de la doublure) 

Par défaut toutes les méthodes de la classe d'origine sont remplacées par une implémentation renvoyant "null".

### Les dépendances de test
Elles sont de différentes natures : 
* API (située hors de l'application)
* Base de données
* FileSystem
* etc.

Ces dépendances nécessitent une setup et une configuration en prérequis de l'exécution des tests.
Elles peuvent êtres substitués ce qui apporte du confort (ex: vitesse d'exécution des tests).

### Granularité des tests 

Deux écoles existent : école classique VS école de Londres, deux pensées de l'approche de l'isolation :  
* Définition du terme "Unitaire" (unit) et de la taille d'une unité. Est-ce constitué par une classe ou un set de classes ? 
* Utilisation des doubles. Quand utiliser des doubles pour les tests ?
 

Retenir => L'idée est de tester un **comportement** qui a du sens pour le domaine, idéalement identifiable comme utile pour une personne du métier.


## Test-Driven Development (TDD)

- TDD: process de conception de logiciels qui repose sur le test pour conduire le développement d'un projet. 
- Le process se dissocie en 3 étapes : 

1) Ecriture d'un test en échec. Cela indique la fonctionnalité à implémenter et comment elle doit se comporter.
2) Ecriture du code, pour faire passer le test. A ce stade, le code ne doit pas nécessairement être raffiné.
3) Refactorisation du code. Avec la protection du test unitaire, il est sûr de nettoyer le code pour le rendre davantage lisible et maintenable. 

## Tests impliquant une BDD

**Problématique:** L'accès aux données est liée à des librairies d'abstraction (PDO, Doctrine etc.) 
L'extension DBUnit vise à simplifier les tests avec ces librairies.

4 phases d'un TU : 
* Configurer une fixture. L'état initial de la BDD / de l'application au moment de l'exécution du test. 
* Expérimenter le système à tester 
* Vérifier les résultats 
* Nettoyer

NB: Symfony permet de spécifier l'exécution des commandes Doctrine (création BDD, création des schémas/tables, chargement des données) 
sur l'environnement de test.

## Structure d'un test unitaire 

Le test unitaire suit généralement un pattern équivalent à :
* **Given (arrange)**: Mettre le système à tester (SUT) et ses dépendances dans un état désiré.
* **When (act)**: Appel de méthodes du SUT, passage des dépendances et capture de la sortie (si elle existe). 
* **Then (assert)**: Vérification de la sortie. La sortie, peut être représentée par le statut du retour.
