# Value vs Ref

## Data types

The latest ECMAScript standard defines seven data types:
Values can be partitioned into two main kinds: primitives and objects.

Seven data types, 6 are what we call primitive;
    **primitives**:
        - Boolean
        - Null
        - Undefined
        - Number
        - String
        - Symbol (new in ECMAScript 6) 


### Primitives are immutable;
```
var fruit = 'banana';
fruit.age = 28; // write - ignored
console.log(fruit.age) // read - undefined

var babyFruit = 'banana'
babyFruit[0] = 'n'; // write - ignored
console.log(babyFruit); // read - 'banana'
```

### Primitives are compared by value

To compare primitives, JS looks at their content. If the content(values) are the same, then they are considered equal.

```
'hello' === 'hello'
'hi' === 'hello'
true === false
undefined === null
```

For primitives, variables contain the value which means that when you copy one variable into the other, it will create a copy of the content/ the **value**

```
var a = 'woo'
var b = 'foo'
```

```
a === b

var a = 'jellyMountain';
var b = a;
a = 'peanutButter';
```

what does a equal?
what does b equal?

Show on board

```
var a = 10;
var b = a;
a = a * 2;
```

what does a equal?
what does b equal?

Show on board

## Object data types

Objects can be partitioned further:

    - Creatable by literals. The following literals produce objects that can also be created via constructor. Use literals whenever you can.
        - [] is the same as new Array()
        - {} is the same as new Object()
        - function() {} is the same as new Function()

### Objects are mutable by default:
    var me = {name: 'Sam'};
    me.age = 29; // write
    console.log(me.age) // read

### Objects are compared by reference

For objects (including arrays and functions), JS stores a reference to where the object is stored in memory.

Every object you create via an expression such as a constructor or a literal is considered different from every other object; a fact that can be observed via the equality operator (===). That operator compares objects by reference: two objects are only equal if they have the same identity. It does not matter whether they have the same content or not.

So when we create an object and store it in one variable and then we copy that variable into a new variable, it doesn't copy the value like it did with primitives. Instead it copies the reference. The pointer to where the object is being stored in memory.

i.e. 

var a = {name: 'Sam'}
b = a;
a.age = 29;

What does a equal?
what does b equal?

Why?
Does a === b?

Show on board that var a points to an object and b points to the same obj so if a changes so does b.

It does because they point to the same object. For 2 variables containing objects to be equal, they must be pointing to the same object.

Different objects containing same info

var a = {name: 'Daryl'}
var b = {name: 'Daryl};
a.age = 28;

What does a equal?
What does b equal?
Does a === b?

Why?

Show on board creation of two seperate objects in memory therefore are not the same as to be equal must point to the same object.

## Arrays

var a = [1, 2, 3];
b = a;
a === b?

Second example 

var a = [1, 2, 3];
b = [1, 2, 3];
a === b?

Why?

As arrays are a type of object, it works the same way as an object.

## Copying an object without copying its reference

Does anyone know how to do this with an array? 

I can create a new array, with a new reference and modify it without modifying the original by using slice.

eg. 

```js
const people = ['Sam', 'Mauro', 'Harriet', 'Mitch', 'Jonny']

const tutors = people.slice()

tutors.push('JD')
```

To do this with an object, I need to use object.assign. So let's say I have the following data available. I want to change age to date of birth without mutating the original array. 

Let's work this out together.

```js
 const people = [
     {
         name: 'Sam', 
         age: 29
     },
     {
         name: 'Jonny',
         age: 31
     },
     {
         name: 'Mitch',
         age: 27
     }
 ]


const newPeople = people.map((person) => {
    const newPerson = Object.assign({}, person)
    newPerson.dob = 2017 - newPerson.age;
    delete newPerson.age;
    return newPerson;
})


```

## Summary

- What are primitive values in JS?
- What other data types are there?

- When you copy a primitive, it copies the value into the new variable.
- When you copy an object, it copies the reference into the new variable.
- For primitives to be ===, the value must be the same. i.e. 'banana' === 'banana'.
- For objects to be ===, the reference must be pointing to the exact same object

## Reading 

- http://2ality.com/2011/03/javascript-values-not-everything-is.html

