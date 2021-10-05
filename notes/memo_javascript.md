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
(Gros intérêt du TypeScript qui va permettre un typage strict).

## Fonction `typeof`
Voir le type : string, number, function etc.

## Primitive data types (immutable)

- Boolean
- Null
- Undefined
- Number
- String 
- Symbol (new with ES6)

**Ne pas utiliser le null => null est un object , déconseillé, il vaut mieux utiliser undefined**

## Mutable data type for items

- Object

## Falsy values (evaluated to false by interpretor)
- false 
- 0
- ""
- NaN
- undefined 
- null

## Using Spread operator to copy values from an array to another, w/t ref problem

```javascript

let a = ["b","c","d"];
let b = a ;

a.splice(0,1);
console.log(b);
// now b = ["c","d"];

let c = [...a];
a.splice(0,1);
// c still has ["c","d"];
console.log(c);
// a returns ["d"];
console.log(a);

```


## 'Own' properties versus 'Prototype' properties

```
Own properties are defined directly on the object instance itself. (thus, duplicated for all objects instancied)
function verifying condition is : hasOwnProperty(thePropName)

Whereas , Prototype properties are defined on the prototype itself, and shared amongst all Object of the same type.
```

## Prototype inheritance
```
An objet inherits its behavior from another object by refering its prototype object
ChildObject.prototype = Object.create(ParentObject.prototype);

Child object receive its own methods by chaining them onto its prototype
ChildObject.prototype.methodName = function() {...};

javascript engine will try to resolve a method following the prototype chain, eg: 

let duck = new Bird();
duck.eat()



    duck => Is eat() defined here? No.
    Bird => Is eat() defined here? => Yes. Execute it and stop searching.
    Animal => eat() is also defined, but JavaScript stopped searching before reaching this level.
    Object => JavaScript stopped searching before reaching this level.



```
