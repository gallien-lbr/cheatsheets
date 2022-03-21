# Test automatisé

dernière mise à jour : 21/03/2022

## PHP et PHPUnit
phpUnit: framework de référence pour le test unitaire en PHP.

### Installation via Composer

```
composer require phpunit/phpunit
```

### Lancer les tests PHPUnit

#### Executer la suite de tests
`vendor/bin/phpunit`

#### Executer la suite de tests avec reporting HTML
`vendor/bin/phpunit --coverage-html coverage`

#### Executer une classe de tests
`vendor/bin/phpunit tests/[fichierTest.php]`

#### Configurer son environnement de test

La configuration se fait via un fichier XML.
`phpunit.xml.dist`

## Ecrire un test 

Pour écrire un test, il suffit de faire hériter sa classe de la classe de tests du framework PHPUnit.

```
// appel du namespace
use PHPUnit\Framework\TestCase;

class MaClasseTest extends TestCase
{
...
}
```

## Spécifités des sous Symfony 

Symfony introduit des classes de plus haut niveau, au dessus de PHPUnit, ex: 
* class `WebTestCase`  
* class `KernelTestCase`

Des commandes permettent de générer une BDD de tests ou encore, de générer automatiquement la structure des classes de tests (voir documentation Symfony).


## De pourquoi à tester à comment tester ? 
Test unitaire s'inscrit dans une démarche qualité.
Aujourd'hui, la question "pourquoi tester ?" ne se pose plus tellement dans le cadre d'un projet à grande échelle. 

Lorsque la codebase évolue avec le temps, l'implémentation de nouvelles fonctionnalités, introduisent plus de difficultés (bugs, régresssions), et donc pour une valeur métier équivalente, on va déployer plus d'énergie qu'au début du projet.
Le testing automatisé propose une réponse à cette problématique. (voir objectifs).

## Objectifs

4 piliers du TU : 
  * **Feedback rapide**
  * **Maintenabilité**
  * **Protection contre la régression**
  * **Résistance au refactoring**
 
## Promesses et bénéfices attendus

* Relever / résoudre des problèmes de conception ou mauvais pattern, lors de l'écriture des tests. (Corollaire: un code mal conçu ne pourra pas être testé, ou difficilement.)
* Lever un avertissement en cas de régression sur une fonctionnalité, avant le déploiement en production
* Gagner en confiance dans son code. Pouvoir refactoriser, réorganiser son code sans crainte de casser le fonctionnement existant.

 
 ## Catégories de tests
 
 * **Test unitaire**: s'assurer qu'une partie individuel du code se comporte comme prévue.
 * **Test d'intégration**: Tester une combinaison de classes qui interéagissent entre elles (avec le service container par ex. sur Symfony).
 * **Test application**: Tester le comportement d'une application complète. Il s'agit de faire une requête HTTP (réel ou simulé via un Crawler),
 * et tester la réponse attendue. 
 
 
 ## Concepts
 
 ### Etat d'une suite de tests PHPUnit 
 
 * ```OK (n Tests, y assertions)```
 * ```Failure```
 
 ### Taux de couverture du code 
 
 Un indicateur basé sur la formule simple : 
 
 `Couverture de test = Nb Lignes Executées (code) / Total de lignes (tu)`
 
 Un indicateur peu fiable, qui ne présume pas de la qualité des tests et de la pertinence des cas soumis aux tests.
 Il faut retenir que tester l'application dans l'objectif d'une couverture à 100% n'a pas de sens. Il s'agit plutôt de cibler les zones critiques, 
 dont le métier va dépendre.
 
 ### Définition d'une suite de tests efficace
 
 * Intégrée au cycle de développement, donc exécutée à chaque modification de code. (les tests ne servent à rien sinon)
 * Cible les parties les plus importantes du code.
 * Produit un maximum de valeur pour un minimum de coût de maintenance.

### Mock et doublure de test

Le **mock** fournit une doublure de test, qui permet de substituer un objet dont la classe à tester (ou SUT) est dépendante.
Nous pouvons coder son comportement et rendre ses sorties prédictibles. 

#### Méthodes de création de Mocks spécifiques à PHPUnit
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

### Approches de l'écriture des tests

2 paradigmes existent : **école "classique"** VS **école de "Londres"**, deux pensées différentes, dans leur approche de l'isolation et de la granularité des tests.

* Définition du terme "Unitaire" (unit) et de la taille d'une unité. Est-ce constitué par une classe ou un set de classes ? 
* Utilisation des doubles. Quand utiliser des doubles pour les tests ?

#### Concepts de l'école de "Londres"

* Les tests ne vérifient qu'une seul classe à la fois.
* Les dépendances sont remplacées par des Doubles de test (ex: Mock)
* En cas d'échec du test, le suspect est désigné automatiquement comme la classe en cours de test

#### Concepts de l'école "Classique"

Le système de tests se base sur des objets "concrets" et non des doubles de tests.
Ce paradigme induit de re-créer le graphe de dépendances complet de l'application (à l'exception de certaines dépendances partagées) pour mettre en place le système de test automatisé.  

#### A retenir
L'idée est de tester un **comportement** qui a du sens pour le domaine, idéalement identifiable comme utile pour une personne du métier.


## Test-Driven Development (TDD)

- TDD: process de conception de logiciels qui repose sur le test pour conduire le développement d'un projet. 
- Le process se dissocie en 3 étapes : 

1) Ecriture d'un test en échec. Cela indique la fonctionnalité à implémenter et comment elle doit se comporter.
2) Ecriture du code, pour faire passer le test. A ce stade, le code ne doit pas nécessairement être raffiné.
3) Refactorisation du code. Avec la protection du test unitaire, il est sûr de nettoyer le code pour le rendre davantage lisible et maintenable. 

L'approche est ici centré sur la résolution du problème. La réflexion est de savoir quel comportement doit être mis en place ? 
L'implémentation de la solution au problème arrive dans un second temps. 

## Tests impliquant une BDD

**Problématique:** L'accès aux données est liée à des librairies d'abstraction (PDO, Doctrine etc.) 
L'extension DBUnit vise à simplifier les tests avec ces librairies.

**4 phases d'un TU avec BDD :** 
* Configurer une fixture. L'état initial de la BDD / de l'application au moment de l'exécution du test. 
* Expérimenter le système à tester 
* Vérifier les résultats 
* Nettoyer

NB: Symfony permet de spécifier l'exécution des commandes Doctrine (création BDD, création des schémas/tables, chargement des données) 
sur l'environnement de test.

## Structure d'un test unitaire 

Le test unitaire suit généralement un pattern équivalent à :
* **Given (arrange)**: Mettre le système à tester (SUT) et ses dépendances dans un état désiré.
* **When (act)**: Appel de méthodes du SUT (invoque la méthode réelle testée), passage des dépendances et capture de la sortie (si elle existe).  (bonne pratique => 1 ligne)
* **Then (assert)**: Vérification de la sortie. La sortie, peut être représentée par le statut du retour.

### Sections setUp et tearDown

Ces méthodes permettent de mettre en place l'environnement de test (setUp) et de nettoyer l'environnement de test après **chaque** exécution de test. 
Le tearDown est utilisé par exemple pour : 
* Fermer une connexion vers la DB;
* Supprimer des fichiers crée par le test;

### Bonnes pratiques de test unitaire (PHPUnit) 

#### Méthode
Par défaut, les tests automatisés doivent obligatoirement comporter le mot clé **"test"** pour être reconnues et exécutées par le framework PHPUnit. 

Exemple de proposition de nommage : 

`test[Scenario][Fail|Success|Valid|Invalid...]`

- Où scénario décrit en anglais le cas testé, et en dernier l'état attendu (. 

Il peut-être tentant d'utiliser le nom de la méthode du SUT dans le codage des tests. 
Or un inconvénient majeur découle de cette pratique, puisque cela crée un couplage plus fort entre le SUT et le système de test. 
Ex: si on renomme la méthode dans le SUT, il faut automatiquement renommer la méthode du Test, pour conserver une cohérence. 
 
Une pratique proposée, en général est d'utiliser un **nom de comportement**. 
L'exception qui déroge à cette règle, est le code "utilitaire" qui n'a pas de valeur métier, on pourra alors utiliser le nom de la méthode du SUT. 
L'avantage de choisir un nom de comportement, est qu'il décrit un scénario qui sera même compréhensible quelqu'un du métier, non-développeur.

#### Classe et répertoire de tests

Par convention, on se proposera de nommer la classe de test: 
`MaClasseTest.php`

On observera qu'il s'agit davantage d'un point de départ, que de restreindre le test à la classe `MaClasse.php` du SUT. 
Les tests unitaires pourront s'étendre à d'autres classes.
Il faut garder en tête que l'on cherche à tester un comportement ("Unit of Behaviour") pertinent d'un point de vue Métier. 
et non une unité de code (ou classe dans notre cas). 

#### Tests avec paramètres : fournisseurs de données

Lorsque l'on test un comportement du SUT, qui réagit différement selon les valeurs d'un jeu de données, on peut utiliser en paramètre un fournisseur de données via l'annotation `@dataProvider`.
Le test est ainsi "alimenté" en données, et sera joué sur chaque valeur donnée en paramètre. 
L'intérêt est de regrouper ce qui pourrait être écrit dans différent test, avec un seul test qui est joué sur toutes les valeurs du `dataProvider`.

### Que faut-il tester ? 

Il est inutile de tester des méthodes triviales (ex: une fonction qui return sur 1 ligne), comme un Getter/Setter. 
```
public function getProperty():string 
{
  return $this->property;
}
```
Elles laissent peu de place au doute et à l'introduction d'un bug ou d'une régression. 

En revanche, il est intéressant de tester des méthodes du domaine métier, qui représentent des logiques complexes.
C'est précisement la partie des fonctionnalités critiques que l'on cherchera à couvrir, afin de se prémunir des bugs importants.

### Comment faut-il tester ?

Règle d'or: Ne pas se baser sur l'implémentation dans le SUT, mais tester le résultat attendu en sortie. 
Conséquence directe: éviter des faux-positifs lors de la refactorisation du SUT.

### Les états positifs/négatifs d'un test

* 🔴 Un **"faux-positif"** (= fausse alerte) est un test qui va indiquer un échec alors que le code se comporte comme attendu. 
Cela peut se produire à divers moments (refactorisation, nouveau code).

* 🔴 Un  **"vrai-positif**, est un test qui va remonter un échec réel de la fonctionnalité (état KO). 
* 🟢 Un **négatif** est un test qui va indiquer un test OK 
