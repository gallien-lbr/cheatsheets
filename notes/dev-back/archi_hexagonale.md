# prise de notes conf. AFUP - Architecture Hexagonale

vision architecture hexagonale = comme un port usb 

isoler la partie dédie au métier (domain), survivre aux changements technique 
le reste = infrastructure

dans le métier (domain) décrire des ports 
![2023-12-11_16h06_55](https://github.com/gallien-lbr/cheatsheets/assets/1328920/e80509f8-815a-46dc-996e-4d09038d136f)

------------
Règles d'Or
------------
- Domain n'appelle pas ce qui est dans l'Infrastructure
- Domain n'utilise aucun Namespace externe

-------------
Avantages 
-------------
- repousser dans le temps les décisions architectures
- démonstration plus rapide
- montées de versions fwk et lib + faciles
- tests / bascules de nouvelles lib / services

- tests sont plus simples à écrire

Limites : 
Plus de code à écrires
Outils de génértion de code limités (ex: symfony maker)

à réserver aux applications complexes ou applications qui vont le devenir

Détermination de la complexité d'une application ? core value pour le business ?

Architecture hexa souvent mélé avec du CQRS, clean architecture etc..

Implémentation libre par le développeur de l'architecture Hexa.

```
Exemple arborescence cible: 
src 
 - Domain
 - Infrastructure
 
Pour ce qui est lié au fwk 
Infrastructrure/Symfony 

Pour le domaine, exemple :
Domain/Entity 
```

use Domain\
ne pas mélanger Domain et Infrastructure
