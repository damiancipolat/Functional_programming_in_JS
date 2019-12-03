<img src="https://github.com/damiancipolat/Functional_programming_in_JS/blob/master/doc/fp.png?raw=true" width="125px" align="right" />

# Functional programming in Javascript
Well, I build this repository, because I consider it necessary to give my opinion based on my experience on how it is the best way to **check data types** in our projects using javascript. I think that JS is a great language that today is changing many ways of how to program, all this makes many programmers the lack of a static type checking system in variables at the time of compilation, causes in many people fear and uncertainty on how to handle certain aspects of an application

### In this repository we will learn about this concepts:
- Lazy
- Monoid
- Monad
- Functor
- Curry
- Lambda
- Recursion
- Closure
- Stateless
- Compose
- High order functions
- Pure functions
- First Class
- Side effects


## Lazy evaluation

**Definition**:

Lazy evaluation, or call-by-need is an evaluation strategy which delays the evaluation of an expression until its value is needed (non-strict evaluation) and which also avoids repeated evaluations.

**Code example**:

Lazy evaluation is the process of deferring the evaluation of an expression until later, and this can be done with thunks.

**Example 1:**
```js
// Not lazy
var value = 1 + 1  // immediately evaluates to 2

// Lazy
var lazyValue = () => 1 + 1  // Evaluates to 2 when lazyValue is *invoked*
```

**Example 2:**
```js
// Not lazy
var add = (x, y) => x + y
var result = add(1, 2)  // Immediately evaluates to 3

// Lazy
var addLazy = (x, y) => () => x + y;
var result = addLazy(1, 2)  // Returns a thunk which *when evaluated* results in 3.
```

**Example 3:**
```js
// Curried add (not lazy)
var add = x => y => x + y
var add3 = add(3)
var result = add3(7)  // Immediately evaluates to 10
```

**Example 4:**
```js
// Not lazy
var callApi = spec => fetch(spec.url, spec.options);
var result = callApi({url: '/api', options: {}});

// Lazy
var callApiLazy = spec => () => fetch(spec.url, spec.options);
var result = callApiLazy({url: '/api', options: {}});
```

## Monoid:

**Definition**:

It describes a set of elements which has 3 special properties when combined with a particular operation, often named **concat**.

- The operation must combine two values of the set into a third value of the same set. If a and b are part of the set, then concat(a, b) must also be part of the set. In category theory, this is called a magma.

- The operation must be associative: concat(x, concat(y, z)) must be the same as concat(concat(x, y), z) where x, y, and z are any value in the set. No matter how you group the operation, the result should be the same, as long as the order is respected.

- The set must possess a neutral element in regard to the operation. If that neutral element is combined with any other value, it should not change it. concat(element, neutral) == concat(neutral, element) == element.

**Code example**:

Monoid examples, could be STRING concat, NUMBER addition, FUNCTIONS composition, Async composition.

**Example 1 - Strings:**
```js
const concat = (a, b) => a.concat(b);

concat("hello", concat(" ", "world")); // "hello world"
concat(concat("hello", " "), "world"); // "hello world"

concat("hello", ""); // 'hello'
concat("", "hello"); // 'hello'
```

**Example 2 - Numbers**
```js
(1 + 2) + 3 == 1 + (2 + 3); // true

x + 0; // x
```

**Example 2 - Functions**
```js
const compose = (func1, func2) => arg => func1(func2(arg));

const add5   = a => a + 5;
const double = a => a * 2;

const doubleThenAdd5 = compose(add5,double);
doubleThenAdd5(3); // 11
```

## Monad:

**Definition**:

5555555555555555555

**Code example**:

444444444444444444444444444444444444444.
 
**Example 1:**
```js
111111111111111111111111111111111
```

## Functor:

**Definition**:

A functor is simply something that can be mapped over. Is anything that can be use a map, in practice a functor represents a type that can be mapped over..

**Code example**:

 In other words, is any object we can **MAP** and apply a function generating another object instance of the same type and connections.
 
**Example 1:**
```js
[1, 2, 3].map(val => val * 2); //generates [2, 4, 6], Array  is a functor.
```

**Example 2:**
```js
// A map of Number -> String
const numberToString = num => num.toString()
```

**Example 3:**
```js
const Identity = value => ({
  map: fn => Identity(fn(value)),
});
const myFunctor = Identity(1);
myFunctor.map(trace); // 1
myFunctor.map(myFunction).map(trace); // 2
```

## Pure functions:

**Definition**:

A function is a process which takes some input, called arguments, and produces some output called a return value.

**Code example**:

 There are Impure and pure functions, if a function modify something extern to the return cause a side effect.
 
- Given the same input, will always return the same output.
- Produce no side effects.
 
**Example 1:**
```js
//Some examples of pure functions.
const add = (x, y) => x+y;
const sub = (x, y) => x-y;

//Not pure functions
let tmp = 2;

const concat = (a,b)=>{
 tmp = 3;
 return a+b;
};
```

**Example 2:**
```js
const double = x => x * 2;
```

**Example 3:**
```js
function add(a, b) {
  return a + b;
}

function mul(a, b) {
  return a * b;
}

let x = add(2, mul(3, 4));
```

## Side effects:

**Definition**:

A side effect is any application state change that is observable outside the called function other than its return value.

- Modifying any external variable or object property (e.g., a global variable, or a variable in the parent function scope chain).
- Logging to the console.
- Writing to the screen.
- Writing to a file.
- Writing to the network.
- Triggering any external process.
- Calling any other functions with side-effects.

**Code example**:

Side effects are mostly avoided in functional programming, which makes the effects of a program much easier to understand, and much easier to test.

**Example 1:**
```js
let default = '';

const run = ()=>{
 default = '1111;
 return 'aaaaaaaa';
}

run();
```

**Example 2:**
```js
let counter = 0;

const sum = (a,b)=>{
  counter++;
  return a+b;
}
```

## Referential transparency:

**Definition**:

In programming, referential transparency is generally defined as the fact that an expression, in a program, may be replaced by its value (or anything having the same value) without changing the result of the program. This implies that methods should always return the same value for a given argument, without having any other effect.

**Code example**:

Side effects are mostly avoided in functional programming, which makes the effects of a program much easier to understand, and much easier to test.

**Example 1:**
```js
int add(int a, int b) {
    return a + b
}

int mult(int a, int b) {
    return a * b;
}

// 1) The expression is add(2, mult(3, 4)).
// 2) If we replace mult(3,4) with his result 12.
// 3) We can make this add(2, 12) === add(2, mult(3, 4))
```

## High order functions:
Functions that receive an other functions as input/output.

## Recursion:
Dont iretate: use map, filter, reduce.
avoid mutation data:avoid tp change data, make or use a function to return a new data, but modify directly.}
persiste data structures for inmutability, example inmutable js or use this id of the tree. mori / inmutable.js

## Closure:
A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment). In other words, a closure gives you access to an outer function’s scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.
https://developer.mozilla.org/es/docs/Web/JavaScript/Closures

## Stateless:
Stateless programming is a paradigm in which the operations (functions, methods, procedures, whatever you call them) you implement are not sensitive to the state of the computation. That means all the data used in an operation are passed as inputs to the operation, and all the data used by whatever operations invoked that operation are passed back as outputs. In practice, this means the program must have Value semantics (it is not permitted to modify shared/aliased data structures, and objects do not have an identity), must not use global or class variables, and all input/output must be handled specially (such as through monads or by threading an I/O state through any parts of the computation that perform I/O). Exception handling may also make the computation stateful.

## Compose:
Combine, functions' effects to create a pipeline through which our program's data can flow through.

## Curry

**Definition**:

5555555555555555555

**Code example**:

444444444444444444444444444444444444444.
 
**Example 1:**
```js
111111111111111111111111111111111
```

## Lambda:

**Definition**:

5555555555555555555

**Code example**:

444444444444444444444444444444444444444.
 
**Example 1:**
```js
111111111111111111111111111111111
```

## The resources come from this websites and talks

Specialy from Anjana Vakil - **JSCONF**:
- http://2016.jsunconf.eu/
- http://bangbangcon.com/speakers.html#anjana-vakil

Others websites:
- https://teamtreehouse.com/community/what-is-a-lambda-in-javascript
- https://medium.com/front-end-weekly/implementing-javascript-functors-and-monads-a87b6a4b4d9a
- https://marmelab.com/blog/2018/04/18/functional-programming-2-monoid.html
- https://codewords.recurse.com/issues/four/lazy-composable-and-modular-javascript
- https://www.tutorialspoint.com/functional_programming/functional_programming_lazy_evaluation.htm
- https://www.youtube.com/watch?v=-tndyOuK7z8
- https://www.youtube.com/watch?v=q2NgcoXki7o
- https://github.com/vakila/functional-workshop
- https://speakerdeck.com/vakila/first-steps-into-functional-programming
- https://www.codingame.com/playgrounds/2980/practical-introduction-to-functional-programming-with-js
- https://hackernoon.com/function-type-signatures-in-javascript-5c698c1e9801
- https://marmelab.com/blog/2018/04/18/functional-programming-2-monoid.html
- https://developer.mozilla.org/es/docs/Web/JavaScript/Closures
- https://www.codementor.io/agustinchiappeberrini/lazy-evaluation-and-javascript-a5m7g8gs3
- https://hackernoon.com/lazy-evaluation-in-javascript-84f7072631b7
- https://stephen-young.me.uk/2013/01/20/functional-programming-with-javascript.html
- https://marmelab.com/blog/2018/09/26/functional-programming-3-functor-redone.html
- https://marmelab.com/blog/2019/03/20/functional-programming-4-art-of-chaining-monad.html
