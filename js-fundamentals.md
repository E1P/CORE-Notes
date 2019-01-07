# JS Fundamentals

## What happens when JS runs my code?

What happens when we run Javascript?

* It reads it line by line. In v8 it uses just-in-time compilation.
* It assigns data to variables in memory.

```js
const arr = [1, 2, 3];
function sayHello(name) {
  const str = 'hello ' + name;
  return str;
}
const me = 'Sam';
```

So let's go through line by line:

What happens first?

1. arr is created in global memory, with the array stored there.
2. sayHello is created in global memory
3. me is created in global memory

Why aren't we interested in the body of the function? Because the function was never called. Everything in there is hypothetical. What would str be? It doesn't make sense to store hypotheticals.

So, how can we run this code? We're going to do it in Node.

What happens when we do? We create a global execution context. It's global because we're running the whole file.

So we execute our code, which starts something called a 'thread of execution'. How many things can that do at a time? 1. Javascript is a single threaded language.

Which order do we do these things? Synchronously.

So let's talk about calling/invoking a function. Say I wanted to take say hello and call it with my name. How do I invoke a function? All I need to do is add parentheses.

Do I need to put anything in the parentheses? No. The function might not behave without arguments - but it will run.

```js
const arr = [1, 2, 3];
function sayHello(name) {
  const str = 'hello ' + name;
  return str;
}
const me = 'Sam';
const output = sayHello('Mitch');
```

So say I've done this. How is my global memory updated?

4. output is created in global memory.

What is it set to? Initially, undefined. Why? We need to wait for the function to run!

So in order to assign our output, we need to see what happens when I call sayHello. Where do we call sayHello? Global execution context. What happens when we do? It creates an execution context of its own.

Just like our global has a global memory and a global threat, A local execution context has a local memory and a local thread.

So what happens now?

5. In local memory, we create a variable called 'name', which was specified as a parameter to our function. We assign it whatever the value of the first argument was. What would it be if I called this function without an argument?
6. In local memory, we create the str by concating hello to name.
7. We return this value from the function, which ends the function and sets our output in global memory.

So, let's make sure go this down. Let's complicate this example a little.

```js
const arr = [1, 2, 3];
function sayHello(name) {
  const str = 'hello ' + name;
  return str;
}
function timesTwo(num) {
  const result = num * 2;
  return result;
}
const me = 'Sam';
const output = sayHello(me);
const output2 = timesTwo(4);
```

Let's walk through what happens now:

1. arr is created in global memory
2. sayHello is created in global memory
3. timesTwo is created in global memory
4. me is created in global memory
5. Output is created, it's set to undefined
6. sayHello is called in the global execution context.
7. it creates a local execution context. In here we have a local memory and thread.
8. We create a variable called name. Why? This is the parameter we created our function with. What value is assigned to it? The value of me, which is the string Sam.

What's it called when I pass a value into a function invocation? An argument.

What's the difference between a parameter and an argument? Parameters are specified when we define our function - they're placeholders, hypothetical values. Arguments are the actual values we pass into our function.

9. We then create string in local memory - which we create by doing what? Concat-ing 'hello ' to whatever our name is in local memory.
10. We then return str - which sets what? Output in our global.
11. Where does our thread go to now? Back to global.
12. So what happens next? We set output2 to undefined while our thread goes into a new... local execution context.
13. our parameter num is created as a variable, and set as the argument 4.
14. result is set by timesing 4 by 2. To 8.
15. Result is returned, ending our local execution context and setting output2 to 8 in global.
16. Global finishes running.

## The Call Stack

So we are in a situation where with these all execution contexts, it could be difficult to keep track of where we are. And this is incredibly simple code! But it's not just us, how does JS know where its thread is at any one time? How does it know when it needs to return to the global?

It uses a data structure that allows us to track the where we, or the current thread of execution, currently is. Does anyone know what it's called?

The call stack.

_Draw call stack, repeat last example with it._

When we run the file, global is pushed into the call stack. Then when it finds another function invocation, that is pushed in on top. Like a stack of plates. This is also known as a LIFO - last in, first out data structure.

Whatever is on the top of the stack must resolve its thread to completion first. Just like with a stack of plates. We wouldn't take anything off the bottom, or the middle.

So what happens in the call stack when we run the file?

1. Global is pushed in.
2. sayHello is pushed in.
3. sayHello is resolved, so it is popped off.
4. timesTwo is pushed in.
5. timesTwo is resolved, so it is popped off.
6. global is resolved, so it is popped off.

Let's complicate the example a little.

```js
function timesTwo(n) {
  return n * 2;
}
function doubleAge(person) {
  const doubledAge = timesTwo(person.age);
  const olderPerson = {
    name: person.name,
    age: doubledAge
  };
  return olderPerson;
}
const sam = { name: 'Sam', age: 29 };
const olderSam = doubleAge(sam);
```

Let's run through this whole example with the call stack in mind.

1. So, what happens when we run the file? We add global to the call stack, we create a global execution context - with a global memory and thread.
2. We add timesTwo to global memory.
3. We add doubleAge to global memory.
4. We add sam to global memory.
5. We add olderSam to global memory, which is set to what? Undefined for now!
6. We call doubleAge. This creates an execution context and adds doubleAge to the call stack.
7. The person parameter is set as variable in local memory. It's set to the argument. The object sam.
8. We create a variable called doubledAge, which is set to undefined for now.
9. We call timesTwo, which adds timesTwo to the stack, and creates a new execution context.
10. The parameter n is set as a variable in local memory. What is it set to? The argument person.age, which is what? 29.
11. We return n \* 2, which ends closes this execution context and pops it off the stack.
12. We return to the execution context of doubleAge, which now has doubledAge set to 58.
13. We create a variable called olderPerson, with its associate properties.
14. We return olderPerson, which closes this execution context and pops doubleAge off the call stack.
15. Global has finished running, so it's popped off the call stack.

## Recap

* JS runs line-by-line with JIT compilation.
* It is single threaded, which means only one thing can happen at a time.
* The difference between arguments and parameters.
* When a function is called it creates an execution context and its own local memory. The local memory is called a 'variable environment'.
* The call stack keeps track of the thread by pushing things on when they're called, and popping them off when they've resolved.
