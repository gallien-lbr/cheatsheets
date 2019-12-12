# Memo-Javascript

## Primitive data types (immutable)

- Boolean
- Null
- Undefined
- Number
- String 
- Symbol (new with ES6)

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