# Memo-Javascript

# Utilisation versatile du JS aujourd'hui 

* App mobile / application desktop (Electron)
* Création de serveur (NodeJs + Express)
* Scripting bash
* Single Page Application

# Variables et typage
## Let Keyword
Remplace le `var`. Ne stock pas la valeur dans l’objet window.
On ne peut pas redefinir la variable dans chrome, déclarer 2 fois une variable avec let est interdit (norme ES6, à l'exception de la console de debug de chrome qui l'autorise) 

## Mot clé const
Constante.  (on défini en constante la case mémoire)

## Inférence de type
Typage dynamique. La variable va prendre le type en fonction de la valeur qu’on lui donne. 
(Versus le TypeScript qui va introduire le typage strict et donc un meilleurs controle sur les données).

## Fonction `typeof`
Voir le type : string, number, function etc.

## Primitive data types , value type (immutable)

- Boolean
- Null
- Undefined
- Number
- String 
- Symbol (new with ES6)

**Ne pas utiliser le null (comparaison if etc..) => `typeof null` est un object. Donc mieux vaut utiliser `undefined`**

## Reference type (mutable)

- Object
- Array
- Function
ou encore
- Date
- Regex

## Falsy values (evaluated to false by interpretor)
- false 
- 0
- ""
- NaN
- undefined 
- null


```
ref: https://blog.devgenius.io/mutable-and-immutable-in-javascript-78a3cbc6187c
ref : https://hackernoon.com/mutability-and-immutability-in-javascript-explained-in-detail-x7q33ag
