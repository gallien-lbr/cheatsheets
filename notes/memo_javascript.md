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
