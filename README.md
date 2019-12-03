<img src="https://github.com/damiancipolat/Functional_programming_in_JS/blob/master/doc/fp.png?raw=true" width="125px" align="right" />

# Functional programming in Javascript
I have been a javascript programmer for a long time and I have seen this language grow, from a simple tool to validate forms with jquery, to be able to create large backend platforms. Since ES6 appeared and the ability to add "classes" I see that it has only caused a confusion in the way of programming, making a javascript code as a migration from java. 

Since I came across functional programming I saw how it adapts perfectly to the potential of javascript and how it achieves a much better clarity in the way of writing code.

### What is functional programming (FP)?:

In computer science, functional programming is a programming paradigm—a style of building the structure and elements of computer programs—that treats computation as the evaluation of mathematical functions and avoids changing-state and mutable data. It is a declarative programming paradigm in that programming is done with expressions or declarations instead of statements. In functional code, the output value of a function depends only on its arguments, so calling a function with the same value for an argument always produces the same result. This is in contrast to imperative programming where, in addition to a function's arguments, global program state can affect a function's resulting value. Eliminating side effects, that is, changes in state that do not depend on the function inputs, can make understanding a program easier, which is one of the key motivations for the development of functional programming.

https://en.wikipedia.org/wiki/Functional_programming


### In this repository we will learn about this concepts:
- [Lazy evaluation](#lazy-evaluation)
- [Monoid](#monoid)
- [Monad](#monad)
- [Functor](#functor)
- [Curry](#curry)
- [Lambda](#lambda)
- [Recursion](#recursion)
- [Closure](#closure)
- [Stateless](#stateless)
- [Compose](#compose)
- [High order functions](#high-order-functions)
- [Pure functions](#pure-functions)
- [First Class](#first-class-function)
- [Side effects](#side-effects)


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

todo pending

**Code example**:

todo pending
 
**Example 1:**
```js
todo pending
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

**Definition**:

Higher-order functions are functions that take other functions as arguments or return functions as their results.

**Code example**:

In Javascript, functions are values ( first-class citizens ). This means that they can be assigned to a variable and/or passed as a value..

**Example - Map:**
```js
const double = n => n * 2

//The map function is a high order function.
[1, 2, 3, 4].map(double); // [ 2, 4, 6, 8 ]
```

**Example - Filter:**
```js
let isBoy = student => student.sex === 'M';

//Filter is high order function.
let getBoys = grades =>grades.filter(isBoy);
```

**Example - Custom:**
```js
const ivaTax = (a)=> ((a*21)/100);

//Calc is high order function.
const calc = (ammount, tax) => tax(ammount);

//Use
calc(100.50,ivaTax);
```

## First-Class function:

**Definition**:

I think is important to write about this concept, maybe is'nt from a Fp, but is interesting. First-class functions, meaning that functions are treated like any other first-class object — they can be stored in variables, passed around, returned from other functions, and even hold their own properties. Sometimes referred to as a first-class citizen, is an object that supports all of the operations generally allowed to other objects. 

In fact, JavaScript functions are themselves types of objects. A first-class function can thus be expected to support the same operations we would expect from other objects.

- Be stored in a variable.
- Be passed as arguments to functions.
- Be returned by functions.
- Be stored in some data structure.
- Hold their own properties and methods.

**Code example**:

For the JavaScript programmer this means that you can take advantage of powerful design patterns such as higher-order functions, partial function application, callbacks, and more.
 
**Example - stored function:**

```js
const sayHi = (name)=>console.log('HI',name);
sayHi('Damian');
```

**Example - passed as argument:**
```js
const tax = (tax)=>(tax*21)/100;
const buy = (value,taxes)=> value+taxes(value);

//Use
buy(100,tax);
```

**Example - stored in structures:**
```js
const tax = (tax)=>(tax*21)/100;
const buy = (value,taxes)=> value+taxes(value);

const scooter = {
 ammount:100,
 buy,
 tax
};

//Use
scooter.buy(scooter.value,scooter.tax);
```

## Recursion:

**Definition**:

Recursion is a technique for iterating over an operation by having a function call itself repeatedly until it arrives at a result. Most loops can be rewritten in a recursive style, and in some functional languages this approach to looping is the default.

**Code example**:

JavaScript’s functional coding style does support recursive functions, we need to be aware that most **JavaScript compilers are not currently optimized to support them safely**.

We can use **filter**, **map**, **reduce**, **foreach** high order functions to make recursion in JS.
 
**Example 1:**
```js
const countdown = (value) => (value>0)?countdown(value-1):value;
```

**Example 2:**
```js
const factorial = (number) => (number<=0)?1:(number*factorial(number-1));
```

**CAUTION:** 

Could be possible, using this functions to cause a stackoverflow in the call stack of the JS engine. 

**RangeError: Maximum call stack size exceeded:**
```js
countdown(100000)

Uncaught RangeError: Maximum call stack size exceeded
    at countdown (<anonymous>:1:19)
    at countdown (<anonymous>:1:40)
    at countdown (<anonymous>:1:40)
    at countdown (<anonymous>:1:40)
    at countdown (<anonymous>:1:40)
    at countdown (<anonymous>:1:40)
    at countdown (<anonymous>:1:40)
    at countdown (<anonymous>:1:40)
    at countdown (<anonymous>:1:40)
    at countdown (<anonymous>:1:40)
```

**SOLUTION - TRAMPOLINE:**

Exists a technique call **TRAMPOLINE** to solve this situation.

Some links of this topic:
https://eddmann.com/posts/recursive-functions-using-a-trampoline-in-javascript/
https://medium.com/@cukejianya/functional-js-trampolines-tails-88723b4da320
https://en.wikipedia.org/wiki/Trampoline_%28computing%29
https://raganwald.com/2013/03/28/trampolines-in-javascript.html

**Code examples:**
```js

//TRAMPOLINE
const trampoline = (fn) => {
    while (typeof fn === 'function') {
        fn = fn();
    }
    return fn;
};

//Test functions
const odd  = (n) => () => n === 0 ? false : even(n - 1);
const even = (n) => () => n === 0 ? true : odd(n - 1);

//Use
trampoline(factorial(100000)) // BigInt required
```

## Closure:
A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment). In other words, a closure gives you access to an outer function’s scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.
https://developer.mozilla.org/es/docs/Web/JavaScript/Closures

## Stateless:

**Definition**:

Stateless programming is a paradigm in which the operations (functions, methods, procedures, whatever you call them) you implement are not sensitive to the state of the computation. That means all the data used in an operation are passed as inputs to the operation, and all the data used by whatever operations invoked that operation are passed back as outputs.
https://stephen-young.me.uk/2013/01/20/functional-programming-with-javascript.html

**Code example**:

This is a form of function composition since this is the result of the multiplication that is passed to the add function.
 
**Example**
```js
const isEven = x => x % 2 === 0
const filterOutOdd = collection => collection.filter(isEven)

const add = (x, y) => x + y
const sum = collection => collection.reduce(add)

const sumEven = collection => compose(sum, filterOutOdd)(collection)

sumEven([1, 2, 3, 4])
```

## Compose:

**Definition**:

In the most general terms, we can break the whole discipline of programming down into a couple of stages:
- Understanding complex business logic of a problem.
- Bbreaking the problem down to a set of smaller problems.
- Solving the smaller problems one at a time, and putting it back together to form a coherent solution.

**Code example**:

This is a form of function composition since this is the result of the multiplication that is passed to the add function. In maths we know it as the same way: f(x)0g(x) =  f(g(x)), example. f(x)=2x+5 and g(X)=1x+2 => f(g(x))=2.(1x+2)+5
 
**Example - Function composition:**

```js
const isEven = x => x % 2 === 0
const filterOutOdd = collection => collection.filter(isEven)

const add = (x, y) => x + y
const sum = collection => collection.reduce(add)

const sumEven = collection => compose(sum, filterOutOdd)(collection)

sumEven([1, 2, 3, 4])
```

## Curry

**Definition**:

Currying is the process of taking a function with multiple arguments and turning it into a sequence of functions each with only a single argument.

**Code example**:

A curried function is a function that takes multiple arguments one at a time.
 
**Example - Curry 1:**
```js
const notCurry = (x, y, z) => x + y + z; // a regular function
const curry    = x => y => z => x + y + z; // a curry function
```

**Example - Curry 2:**
```js
const divisible = mod => num => num % mod;

//Call
divisible(10)(2);

//Call 2
const divisibleEn3 = divisible(3);
divisibleEn3(10)
```

You can continue riding in this link: https://medium.com/front-end-weekly/javascript-es6-curry-functions-with-practical-examples-6ba2ced003b1

## Lambda:

**Definition**:

Lambda expressions are present in most of modern programming languages (Python, Ruby, Java...). They are simply expressions that create functions. This is really important for a programming language to support first-class functions which basically means passing functions as arguments to other functions or assigning them to variables.

**What is a Lambda?**

In computer science, the most important, defining characteristic of a lambda expression is that it is used as data. That is, the function is passed as an argument to another function, returned as a value from a function, or assigned to variables or data structures. Is a classic in programming language when we talk about lambda use => or -> simbols.

**Lambda vs anonymous functions:**

An **anonymous function** is, as its name implies, a function without a name.

```js
const hello = function(name){console.log('Hi '+name);}

Or using arrow functions
const hello = (name) => {console.log('Hi '+name);}

Other example:
[1,2,3,4,6].filter((num)=>num>=3); //(num)=>num>=3 is an anonymous function

```

A **lambda function** is a function used as parameter:

```js
[1,2,3,4,5,6,7,8].map(e=>({value:e})); //e=>({value:e}) Is a LAMBDA.

$('#el').on('click',()=>{.....});       //Is a LAMBDA and anonymous and arrow function.
$('#el').on('click',function(){.....}); //Is a LAMBDA and anonymous function.
$('#el').on('click',function clickHandler()=>{.....}); //Is a LAMBDA and a named functions.
```

**Code example**:

So a Lambda not always is an anonymous function, looks like some people are still confused, because you've accepted "lambda = anonymous" as gospel. While it is a somewhat useful concept to understand that anonymous functions have interesting uses, such as points-free-style (tacit programming), that is not the salient point of lambdas. It's mostly syntactical sugar.
 
**Example - arrow functions:**
```js
const isChildren = (person)=>person.age<18;
const isTeen     = (person)=>person.age>18 and person.age<25;

const course = [{name:'bob',age:18},{name:'Damian',age:32},{name:'Alexander',age:19}];

//Get childrens.
course.filter(person=>isChildren(person));

//Get teens.
course.filter(person=>isTeen(person));
```

**Example - named functions:**
```js
$('#el').on('click',function clickHandler()=>{.....}); //Is a LAMBDA and a named functions.
```

**Example - anonymousfunctions:**
```js
$('#el').on('click',()=>{.....}); 
```

## The resources come from this websites and talks

Specialy from Anjana Vakil - **JSCONF**:
- http://2016.jsunconf.eu/
- http://bangbangcon.com/speakers.html#anjana-vakil

From many websites:
- https://gist.github.com/ericelliott/414be9be82128443f6df
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
