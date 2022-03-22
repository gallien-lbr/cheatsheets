# Test automatisé

*dernière mise à jour : 22/03/2022*

## PHPUnit
Le framework de référence pour le testing en PHP.

### Installation via Composer

```bash
composer require phpunit/phpunit
```

### Commandes PHPUnit

 Action | Commandes |
|-----------|-----------|
| Executer la suite de tests | `vendor/bin/phpunit` | 
| Executer la suite de tests avec reporting HTML           |     `vendor/bin/phpunit --coverage-html coverage`      |
| Executer une classe de tests          |  `vendor/bin/phpunit tests/[fichierTest.php]`         |

#### Configurer son environnement de test

La configuration se fait via un fichier XML.
`phpunit.xml.dist`

## Ecrire un test 

Pour écrire un test basique, il suffit de faire hériter sa classe de la classe de tests du framework PHPUnit.

```php
// appel du namespace
use PHPUnit\Framework\TestCase;

class MaClasseTest extends TestCase
{
...
}
```

## Spécifités des tests avec Symfony 

Symfony introduit des fonctionnalités supplémentaires en complément de PHPunit.

**De nouvelles classes:**

* Classe: `WebTestCase` pour exécuter des scénarios à la manière d'un navigateur.
* Classe: `KernelTestCase` pour les tests ayants accès aux services Symfony.

**Des commandes** qui permettent de générer une BDD de tests ou encore, de générer automatiquement la structure des classes de tests (voir documentation Symfony).

**De nouvelles assertions.**

Voir doc. Symfony en référence.

L'utilisation des TU sous Symfony nécessite PHPUnit Bridge :
```bash
#composer require symfony/phpunit-bridge
composer require --dev symfony/test-pack
```

##  De la question : "pourquoi à tester" à "comment bien tester" ? 

Le testing automatisé s'inscrit dans une démarche qualité.

Aujourd'hui, la question "pourquoi tester ?" ne se pose plus tellement dans le cadre d'un projet à grande échelle. 

Lorsque la code-base évolue avec le temps, l'implémentation de nouvelles fonctionnalités, introduisent plus de difficultés (bugs, régresssions), et donc pour une valeur métier équivalente, on va déployer plus d'énergie qu'au début du projet.
Le testing automatisé propose une réponse à cette problématique. (voir objectifs).

## Objectifs

4 piliers du testing à mettre en place : 
  * **Feedback rapide**
  * * *Les tests doivent s'exécuter rapidement.*
  * **Maintenabilité**
  * * *Les tests doivent être facilement lisibles et compréhensibles. Ils doivent dépendre d'un minimum de process et composants externes possibles.*
  * **Protection contre la régression**
  * * *Les tests doivent être pertinents pour se prémunir des futurs bugs.*
  * **Résistance au refactoring**
  * * *Les tests doivent être découplés du SUT afin de ne pas engendrer des faux positifs (fausses alertes).*
 
## Promesses et bénéfices attendus

* Lever l'alerte en cas de régression sur une fonctionnalité, avant le déploiement en production.
* Relever / résoudre des problèmes de conception ou mauvais pattern, lors de l'écriture des tests. (Corollaire: un code mal conçu ne pourra pas être testé, ou difficilement.)
* Gagner en confiance dans son code. Pouvoir refactoriser, réorganiser son code sans crainte de casser le fonctionnement existant.

 
 ## Catégories de tests
 
 * **Test unitaire**: s'assurer qu'une partie individuel du code se comporte comme prévue.
 * **Test d'intégration**: Tester une combinaison de classes qui interéagissent entre elles (avec le service container par ex. sur Symfony).
 * **Test application (End-To-End)**: Tester le comportement d'une application complète. Il s'agit de faire une requête HTTP (réel ou simulé via un Crawler) et tester la réponse attendue. En pratique, ce niveau de test implique que l'application soit hébergé pour répliquer l'environnement final. 
 
L'approche "pyramide des tests", propose un certain équilibre des proportions de tests dans un projet, où :
 - **Tests End-To-End** représentent la **minorité** des tests, ils protègent de la régression, mais sont longs à exécuter.
 - **Tests unitaires** prévalent et sont la **majorité**, ils sont rapides en exécution, et facile à maintenir.
 - **Tests d'intégration** se positionnent entre les deux catégories précédentes.

 
 ## Concepts
 
 ### Le SUT - System Under Test
 
 Le SUT d'un point de vue testing, représente tout les acteurs (classes, dépendances etc.) dans un test qui ne sont pas des doublures (stub ou mock).
 
 ### Assertions de tests
 
 Une **assertion** est une expression logique booléenne. 
 Elle retourne la valeur **"TRUE"** lorsque l'expression testée ne provoque aucun bug et donc 
 lorsqu'on obtient le résultat attendu par l'expression.
 
 Elle retourne la valeur **"FALSE"** lorsque l'expression testée provoque un bug.
 
 Exemple:
 ```php
 // act
 $this->client->request('GET', self::API_GET);

 // assert
 $this->assertResponseIsSuccessful();
 $this->assertResponseStatusCodeSame(Response::HTTP_OK);
 ```       
 
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

### Les doublures de test

Le but est d'éliminer les dépendances du système que l'on test, pour faciliter la création des tests automatisés.

**2 catégories de doublure existent:** 

Le **stub** (state based) permettent d'émuler les interactions **entrantes**. Nous pouvons hard-coder le comportement de la doublure et ainsi rendre ses sorties prédictibles. 


Le **mock** (interaction based)  permettent d'émuler et d'examiner les interactions **sortantes**. Objet pré-programmés avec des attentes sur les appels qu'ils vont recevoir. Le **mock** en soit ne retourne pas de valeur mais permet d'examiner que les méthodes de l'objet simulé soient appelées.


#### Outils / méthodes de création des doublures spécifiques à PHPUnit
* `createMock`
* `getMockBuilder` (personnalisation de la doublure) 

Par défaut toutes les méthodes de la classe d'origine sont remplacées par une implémentation renvoyant "null".

NB: Une confusion reigne entre les méthodes de création de **"Mock"** et le type de doublure **Mock**. L'appel aux méthodes de créations Mock, 
permettent indifférement de créer un Stub ou un Mock.


#### Exemples doublures sur PHPUnit 

##### Stub
```php
$stub = $this->createMock(SomeClass::class);
$stub->method('getSomething')
    ->willReturn('foo');

$sut->action($stub);
```

##### Mock
```php
$mock = $this->createMock(SomeClass::class);
$mock->expects($this->once())
    ->method('doSomething')
    ->with('bar');

$sut->action($mock);
```

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

#### Nommage
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
```php
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

### Les états positifs/négatifs d'une suite de tests

* 🔴 Un **"faux-positif"** (= fausse alerte) est un test qui va indiquer un échec alors que le code se comporte comme attendu. 
Cela peut se produire à divers moments (refactorisation, nouveau code).

* 🔴 Un  **"vrai-positif"**, est un test qui va remonter un échec réel de la fonctionnalité (état KO). 
* 🟢 Un **négatif** est un test qui va indiquer un test OK 

**Bonnes pratiques**: à mesure que le projet grandit et afin de s'assurer que l'on peut avoir confiance dans sa suite de tests, il faudra veiller à : 
* **Supprimer les fausses alertes (faux positifs)**
* **Corriger les tests qui ne détectent pas les bugs (faux négatifs)**

## Références
- Unit testing: Principles, Practices and Pattern - Vladimir Khorikov
- [Symfony doc (FR) "Tester"](https://symfony.com/doc/current/the-fast-track/fr/17-tests.html#ecrire-des-tests-unitaires)
- [Symfony doc (EN) "Testing"](https://symfony.com/doc/current/testing.html)
- [PHP Unit](https://phpunit.readthedocs.io)
