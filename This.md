# `this`: 
- The `this` keyword in JavaScript represents the context in which a function is called.
- The context is generally represented by an object.
- `this` gets bound dynamically to the object that is currently calling the method, i.e. at the moment `sayName` is called, `this` inside of it changes to the object to the left of the dot.

`sam.sayHello` -> 'this' is the context of `sam`
`seb.sayHello` -> 'this' is the context of `seb`

Notice how much more efficient our methods are now.

## 4 RULES OF `this` (4th one tomorrow)
- Inplicit binding - we just saw it in action (`console.log(this)` from within the `sayHello` function)

- Default binding:
There are a couple of concepts to cover here, the first one is `GLOBAL` What is global? - it is either node or the browser's window object - `console.log(this)`

Strict mode: `use 'strict'`
`this` becomes `undefined`

- Explicit binding:
Hardly used anymore.
- `bind`
- `apply`
- `call`
This is now what you should take out from this lecture.

## ARROW FUNCTIONS

They do not create their own binding of `this`, which can be extremely useful.
Now we have:
- function declarations - have `this` and hoisted
- function expressions - have `this` and not hoisted
- arrow functions - do NOT have `this`


Example of a factory function

```js

const methods = {
    sayHello: function(){
        console.log(`Hi, my name is ${this.name}`) 
    }
}

function student (name, strengths, favFood) {
    const student = {
      name,
      favAnimal,
      favFood, 
      ...methods, 
    };
    return student;
  }
  const sam = createStudent('Sam', 'pigeons', 'popcorn');
  const seb = createStudent('Seb', 'ant eaters', 'mac n cheese')

  ```