# JavaScript Cheat Sheet 

Based off of [Learn X in Y Minutes](http://learnxinyminutes.com/docs/javascript/).

JavaScript (JS) is a dynamic [interpreted language](#interpreted-lang) that powers the web. It is widely used in browsers (where JS scripts are interpreted by [JavaScript engines](#javascript-engine) like Chrome's [V8](https://developers.google.com/v8/)) and increasingly on servers (on a [Node.js](https://nodejs.org) runtime environment).

JS is a [prototype-based](#prototype-based) scripting language with [first-class functions](#first-class-functions) and [dynamic typing](#dynamic-type). Because of its super flexibility, JS supports multiple styles of programming including [imperative](#imperative), [object-oriented](#object-oriented) and [functional](#functional).

Here's what all those big words above mean: 
- <a name="interpreted-lang"></a>__Interpreted Language__: a language (eg. JS, Python) in which most of its implementations execute instructions directly, without previously compiling a program into machine-language instructions like compiled languages do (eg. C++)
- <a name="javascript-engine"></a>__JavaScript Engine__: a virtual machine that interprets and executes JS
- <a name="prototype-based"></a>__Prototype-Based__: unlike classical OOP with classes and objects, in JS, objects are cloned from other objects, and all objects have _prototypes_ (kinda like the template they inherit from)
- <a name="first-class-functions"></a>__First-Class Functions__:  JS supports passing functions as arguments to other functions, returning them as the values from other functions, and assigning them to variables or storing them in data structures
- <a name="dynamic-type"></a>__Dynamically Typed__: The "type" of all variables is only interpreted at run-time unlike statically typed languages where all variables have a type at compile-time
- <a name="imperative"></a>__Imperative Programming__: Statement based programming
- <a name="object-oriented"></a>__Object-Oriented Programming__: Object based programming
- <a name="functional"></a>__Functional Programming__: Function based programming

## Quick Access Links 
1. [Basics](#basics)
    1. [Primitives](#primitives)
    2. [Operators](#operators)
2. [More Basic Syntax](#syntax)
    1. [Variables](#variables)
    2. [Arrays](#arrays)
    3. [Logic and Control Structures](#logic)
3. [Objects and Functions](#objects-and-functions)
    1. [Objects](#objects)
    2. [Functions](#functions)
    3. [Bind, Call and Apply](#bind)
4. [Function Execution, Variable Scope, Closures & Callbacks](#execution)
    1. [Hoisting](#hoisting)
    2. [Scope Chain](#scope-chain)
    3. [Closures](#closures)
    4. [Callbacks](#callbacks)
5. [Object-Oriented JS and Prototypal Inheritance](#object-oriented)
    1. [Constructors](#constructors)
    2. [Prototypes](#prototypes)
    3. [Prototypal Inheritance](#prototypal-inheritance)
    4. [Built-In Constructors](#built-in)
6. [Bugs and Error Handling](#bugs)
7. [New ES6 stuff](#es6)

TODO: Add 8. Useful Libraries (LoDash, jQuery), 9. Javascript in the browser, 10. NodeJS

<a name="basics"></a>
## 1. Basics 
__Everything__ in JS is either an object or a primitive.
```javascript

// This is a single line comment,
/* and this is a 
multiline comment */

// Semicolons (;) to terminate lines are optional
// However, the JS engine will (usually) automatically insert semicolons upon seeing '\n'
// This can cause some weird behaviour so ALWAYS use semicolons
doStuff();
```
<a name="primitives"></a>
### i. Primitives: Number, String, Boolean (and some special ones) 

```javascript
// JavaScript has one number type (which is a 64-bit IEEE 754 double).
// Doubles have a 52-bit mantissa, which is enough to store integers
//    up to about 9✕10¹⁵ precisely.
3; // = 3
1.5; // = 1.5

// Some basic arithmetic works as you'd expect.
1 + 1; // = 2
0.1 + 0.2; // = 0.30000000000000004 (funky floating point arithmetic--be careful!)
8 - 1; // = 7
10 * 2; // = 20
10 ** 2; // =100 (10 raised to the power 2) same as Math.pow(10, 2)
35 / 5; // = 7

// Including uneven division.
5 / 2; // = 2.5

// Bitwise operations also work; when you perform a bitwise operation your float
// is converted to a signed int *up to* 32 bits.
1 << 2; // = 4

// Precedence is enforced with parentheses.
(1 + 3) * 2; // = 8

// There are special primitive values:
Infinity; // result of e.g. 1/0
-Infinity; // result of e.g. -1/0
NaN; // result of e.g. 0/0
undefined; // never use this yourself. This is the default value for "not assigned"
null; // use this instead. This is the programmer setting a var to "not assigned"

// There's also a boolean type.
true;
false;

// Strings are created with single quotes (') or double quotes (").
'abc';
"Hello, world";

// You can access characters in a string with `charAt`
"This is a string".charAt(0);  // = 'T'

// ...or use `substring` to get larger pieces.
"Hello world".substring(0, 5); // = "Hello"
"Hello world".slice(0, 5); // does the same thing
"Hello world".substr(0, 5); // yet again

// `length` is a property, so don't use ().
"Hello".length; // = 5

// Searching strings
"Mary had a little lamb".search("had"); // returns 5
"Mary had a little lamb".indexOf("zebra"); // returns -1
"Mary had a little lamb".includes("had"); //returns true (ES7). includes() will return true if the parameter provided is in the string, and false otherwise.

// String to a character array
"one two three four".split(" "); // ['one', 'two', 'three', 'four']

// String replace
"happy birthday henry!".replace("h", "H"); // "Happy birthday Henry!"

// ES6 also introduces Symbol as a new primitive type
// But I'll add that on here once I actually figure out what it is
```
<a name="operators"> </a>
### ii. Operators aka weirdly written functions 
```javascript
// Operators have both a precedence (order of importance, like * before +) 
// and an associativity (order of evaluation, like left-to-right)
// A table of operators can be found here 
// https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)

// Negation uses the ! symbol
!true; // = false
!false; // = true

// There's shorthand operators for performing math operations on variables:
someVar += 5; // equivalent to someVar = someVar + 5;
someVar *= 10; // someVar = someVar * 10;

// and an even-shorter-hand  operators for adding or subtracting 1
someVar++; 
someVar--; 

// Strings are concatenated with +
"Hello " + "world!"; // = "Hello world!"

// Comparison Operators
1 < 10; // = true
1 > 10; // = false
2 <= 2; // = true
2 >= 2; // = true

// and are compared with < and >
"a" < "b"; // = true

// Strict Equality is ===
// Strict meaning both type AND value are the same
1 === 1; // = true
2 === 1; // = false

// Strict Inequality is !==
1 !== 1; // = false
2 !== 1; // = true

// == allows for type coercion (conversion) and only checks if the values are equal after coercion
"5" == 5; // = true
null == undefined; // = true

// ...which can result in some weird behaviour...so use === whenever possible
13 + !0; // 14
"13" + !0; // '13true'

// false, null, undefined, NaN, 0 and "" are falsy; everything else is truthy.
// Note that 0 is falsy and "0" is truthy, even though 0 == "0".

// We can use this to our advantage when checking for existence
if (x) { //doSomething };

// Or to set default values
x = x || "default" 
// if x exists, do nothing and short-circuit, else set x to a default

// but a problem arises if x = 0. It exists, but will coerce to false
// be wary of this

// figuring out types of literals and vars
typeof "Hello"; // = "string"
typeof 42; // = "number"
typeof undefined // = "undefined"
typeof null // = 'object' THIS IS A JS BUG!

// figuring out if an object is an instance of another object
// checks all the way down the prototype chain
var x = {}
x instanceof Object // = true
x instanceof Function // = false

```

<a name="syntax"></a>
## 2. More Basic Syntax 
<a name="variables"></a>
### i. Variables 
```javascript
// Variables are declared with the `var` keyword. JavaScript is dynamically
// typed, so you don't need to specify type. Assignment uses a single `=`
// character.
var someVar = 5;

// if you leave the var keyword off, you won't get an error...
someOtherVar = 10;

// ...but your variable will be created in the global scope, not in the scope
// you defined it in.

// Variables declared without being assigned to are set to undefined.
var someThirdVar; // = undefined
```

<a name="arrays"> </a>
### ii. Arrays 
```javascript
// Arrays are ordered lists of values, of any type.
var myArray = ["Hello", 45, true];

// Their members can be accessed using the square-brackets subscript syntax.
// Array indices start at zero.
myArray[1]; // = 45

// Arrays are mutable and of variable length (dynamically sized arrays)
myArray.push("World"); // adds to the end
myArray.length; // = 4

// Add/Modify at specific index
myArray[3] = "Hello";

//ES7 includes() can be used with arrays to check for the presence of a value. it is case sensitive
let names = ["Samuel", "Hamilton", "Eric"];
names.includes("Samuel"); //true
names.includes("samuel"); //false
names.includes("John"); //false
```

<a name="logic"></a>
### iii. Logic and Control Structures 
```javascript
// The `if` structure works as you'd expect.
var count = 1;
if (count === 3){
    // evaluated if count is 3
} else if (count === 4){
    // evaluated if count is 4
} else {
    // evaluated if it's not either 3 or 4
}

// As does `while`.
while (true){
    // An infinite loop!
}

// Do-while loops are like while loops, except they always run at least once.
var input;
do {
    input = getInput();
} while (!isValid(input))

// The `for` loop is the same as C++ and Java:
// initialisation; continue condition; iteration.
for (var i = 0; i < 5; i++){
    // will run 5 times
}

// && is logical AND, || is logical OR
if (house.size === "big" && house.colour === "blue"){
    house.contains = "bear";
}
if (colour === "red" || colour === "blue"){
    // colour is either red or blue
}

// The `switch` statement checks for equality with `===`.
// use 'break' after each case 
// or the cases after the correct one will be executed too. 
grade = 'B';
switch (grade) {
  case 'A':
    console.log("Great job");
    break;
  case 'B':
    console.log("OK job");
    break;
  case 'C':
    console.log("You can do better");
    break;
  default:
    console.log("Oy vey");
    break;
}

```


<a name="objects-and-functions"></a>
## 3. Objects and Functions 
<a name="objects"></a>
### i. Objects 
An object is simply an unordered collection of key-value pairs.
```javascript
// They can be made literally:
var myObj = {key1: "Hello", key2: "World"};
// or using the Object constructor:
var myObj = new Object();

// Keys are strings, but quotes aren't required if they're a valid
// JavaScript identifier. Values can be any type including other objects.
var myObj = {myKey: "myValue", "my other key": 4};

// Objects can even contain functions (called methods)
// When functions attached to an object are called, they can access the object
// they're attached to using the `this` keyword.
var myObj = { 
  name: "Destiny's Child",
  sayMyName: function() {
    console.log(this.name);
  }
}
myObj.sayMyName(); // outputs "Destiny's Child"

// Object attributes can also be accessed using the subscript syntax,
myObj["my other key"]; // = 4

// ... or using the dot syntax, provided the key is a valid identifier.
myObj.myKey; // = "myValue"

// Objects are mutable; values can be changed and new keys added.
myObj.myThirdKey = true;

// If you try to access a value that's not yet set, you'll get undefined.
myObj.myFourthKey; // = undefined

// iterating through objects
for(var property in myObj) { // do something }

// JSON (JavaScript Object Notation) is just a special case of Object literal notation
// where the keys are strings wrapped in quotes
var json_stuff = {
  "firstName": "John",
  "lastName": "Doe",
  "Age": 25
}

// JS Object => JSON
JSON.stringify(myObj);

// JSON => JS Object
JSON.parse(json_stuff);
```

<a name="functions"></a>
### ii. Functions 
Functions are special kinds of objects! Functions can have their own methods and properties just like other objects, but they're rarely used in that way. 

Remember, functions in JS are first-class. Meaning they can be assigned and passed just like any other variable can.

Functions are special in that they have an optional name property and a code property (which is the body of the function that actually does stuff). The function's code is executed by the invocation operator `()`.

```javascript
// JavaScript functions are declared with the `function` keyword.
// This is a function statement
function myFunction(thing){
    return thing.toUpperCase();
}

// This is a function expression
var makeUpperCase = function() {
    return think.toUpperCase();
}

// Note that the value to be returned must start on the same line as the
// `return` keyword, otherwise you'll always return `undefined` due to
// automatic semicolon insertion. Watch out for this when using Allman style.
function myFunction()
{
    return // <- semicolon automatically inserted here
    {
        thisIsAn: 'object literal'
    }
}
myFunction(); // = undefined

// JavaScript functions are first class objects, so they can be reassigned to
// different variable names and passed to other functions as arguments - for
// example, when supplying an event handler:
function myFunction(){
    // this code will be called in 5 seconds' time
}
setTimeout(myFunction, 5000);
// Note: setTimeout isn't part of the JS language, but is provided by browsers
// and Node.js.
```
Function objects don't even have to be declared with a name - you can write an __anonymous function__ definition directly into the arguments of another.

``` javascript
setTimeout(function(){
    console.log("It's been 5 seconds!");
    // this code will be called in 5 seconds time
}, 5000);
```

This has led to a common pattern of __"immediately-executing anonymous functions"__, which prevent temporary variables from leaking into the global scope. The function expression is wrapped in parenthesis and then is invoked using `()`

``` javascript
(function(){
    var temporary = 5;
})();
temporary; // raises ReferenceError
permanent; // = 10
```

An important distinction: primitives __Pass by Value__ while objects __Pass by Reference__
```javascript
// Primitives are passed by value
var i = 2;
function double(i){  i*2;  } // another i is created with the same value in a different execution context
double(i);
console.log(i); // still 2 

// Objects (including functions) are passed by reference
var obj = { hero: "Superman" };
function bestSuperhero(obj){
  obj.hero = "Batman";
}
bestSuperhero(obj);
console.log(obj.hero); // = "Batman"
```
The `this` keyword within methods, always refers to the object that the method is tied to. However, if the method has an inner function, its `this` refers to the global object. Some regard this as a bug in JS, so the good practice is to create and use a variable called `self`.

```javascript
var c = {
    name: 'The c object',
    log: function() {
        var self = this;
        
        self.name = 'Updated c object';
        console.log(self);

        var setname = function(newname) {
            self.name = newname;   
        }
        setname('Updated again! The c object');
        console.log(self);
    }
}
c.log(); // outputs "Updated again! The c object"
```

<a name="bind"></a>
### iii. Bind, Call and Apply 
Functions that aren't tied to objects can use `this` and still be useful. Consider this example.
```javascript
var cow = { says: "moo" };
var dog = { says: "woof" };
var pig = { says: "oink" };

function speak(times) { 
  for(i = 0; i < times; i++) {
    console.log(this.says);
  }
}
speak(4); // error because this is the global object which doesn't have a 'says' property
```
To use speak, we need to use the .bind, .call or .apply methods, which are available to __all__ functions. The first parameter of these functions is the object which becomes `this` within the function.

```javascript
// bind creates a copy of the function it's being called on
var cowSpeak = speak.bind(cow);
cowSpeak(4); // outputs "moo moo"

// call directly executes the function with the first parameter being 'this'
// and all the other parameters being the function's parameters
speak.call(dog, 3); // outputs "woof woof woof"

// apply directly executes the function with the first parameter being 'this'
// and all the other function parameters being passed in as an array
speak.apply(pig, [1]); // outputs "oink"
```
The call and apply methods allow us to do something called __Function Borrowing__.
```javascript
var darthVader = { 
  son: "Luke",
  saying: function(){
    console.log(this.son + ", I am your father");
  }
};
var luke = { son: "Ben" };

darthVader.saying.call(luke);
// borrowing Darth Vader's saying
// outputs "Ben, I am your father"
```
The bind method allows us to do __Function Currying__.
```javascript
// Creating a copy of a function with preset parameters
function multiply(a,b){ return a*b }

// first parameter can be 'this' or null or anything--doesn't matter since 'this' is not used
// the second parameter (a) is permanently set to 2
var double = multiply.bind(this, 2);
double(16); // outputs 32

```

<a name="execution"></a>
## 4. Function Execution, Variable Scope, Closures & Callbacks 

A few important concepts:
- __Global__ means not inside a function. The global object is 'window' in browsers.
- The __Lexical Environment__ is where something sits physically in the code
- __'this'__ is a reference to the object that the currently running method is tied to (by default it's tied to the global object)
- The __Execution Context__ consists of the environment (state of variables) of the function currently being evaluated. It also includes 'this' and a reference to the outer environment (aka what object is sitting outside this function _lexically_)
- The __Execution Stack__ or __Call Stack__ is the "stack" of execution contexts with the global execution context being the bottommost. When the program flow enters a function, a new execution context is popped onto the call stack, and when the function returns, it is popped off.

<a name="hoisting"></a>
### i. Hoisting 
Before actually executing any of the code, the JS engine first looks at all the variable declarations and function statements and sets aside some memory space for them effectively moving them to the top of the code. This is known as __hoisting__.
```javascript
// Variable example

function a(){
  console.log(x);
  var x = 2;
  console.log(x);
}
a(); // outputs 'undefined' then 2

// Function a is essentially equivalent to:
function a(){
  var x; // the var declaration is hoisted up to the top and is set to undefined
  console.log(x); // outputs undefined
  x = 2; // the variable assignment stays. It is NOT hoisted.
  console.log(x); // outputs 2
}

// Function example

a(); // will run properly
b(); // will fail with TypeError because b isn't assigned until line 4
function a() { }
var b = function() { }

The above is equivalent to:
function a() {} // the function statement is hoisted
var b;
a();
b(); // = undefined(); invoking undefined raises an error
b = function() {}
```

JS is always synchronous (executing code 1 line at a time and in-order) and single-threaded (only 1 command at a time). However, jQuery, event handlers and AJAX calls make use of callbacks which appear to run asynchronously. AJAX calls are delegated off to a different part of the browser (outside the JS engine) which is why they are run asynchronously. When the call returns, or if there's a user click, then these events fill up the Event Queue. The JS Engine only handles the Event Queue when the Execution Stack is empty. 

<a name="scope-chain"></a>
### ii. Scope Chain 
To find a variable when functions are running, JS looks further than just the variable environment of the currently executing context, it also looks at the outer environment (the environment to which this function is _lexically_ attached). This process continues looking all the way down to the global environment in a process known as the __scope chain_.

```javascript
function b() {
    console.log(myVar);
}

function a() {
    var myVar = 2;
    b();
}

var myVar = 1;
a();

// function b does not have a myVar variable so it looks to its outer environment
// here, b is lexically attached to the global object, and myVar exists in the global environment
// therefore, it logs '1'


// JavaScript has function scope; functions get their own scope but other blocks
// do not.
if (true){
    var i = 5;
}
i; // = 5 - not undefined as you'd expect in a block-scoped language
```

<a name="closures"></a>
### iii. Closures 
One of JS's most powerful features is __closures__. Whenever a function is nested within another function, the inner function has access to all the outer function's variables even after the outer function exits.
After the outer function exits, it is popped off the Execution Stack, however if any of its variables are referenced in the inner function, then those variables are "closed into" the inner function's Execution Context and are accessible by the inner function.

```javascript
// Example 1

function sayHelloInFiveSeconds(name){
    var prompt = "Hello, " + name + "!";
    // Inner functions are put in the local scope by default, as if they were
    // declared with `var`.
    function inner(){
        alert(prompt);
    }
    setTimeout(inner, 5000);
    // setTimeout is asynchronous, so the sayHelloInFiveSeconds function will
    // exit immediately, and setTimeout will call inner afterwards. However,
    // because inner is "closed over" sayHelloInFiveSeconds, inner still has
    // access to the `prompt` variable when it is finally called.
}
sayHelloInFiveSeconds("Adam"); // will open a popup with "Hello, Adam!" in 5s


// Example 2

function buildFunctions() {
    var arr = [];    
    for (var i = 0; i < 3; i++) {
        arr.push(
            function() {
                console.log(i);   
            }
        )
    }
    return arr;
}

var fs = buildFunctions();
fs[0]();
fs[1]();
fs[2]();
// all 3 of these will log '3' because after buildFunctions finishes, i = 3
// when fs[0..2] are invoked, they look for the value of i and they all see 3

// Avoid creating functions in loops. It will lead to bad behaviour.
```

<a name="callbacks"></a>
### iv. Callbacks 
__Callbacks__ are simply functions passed as arguments to other functions to be run when the other functions are finished.

```javascript
function alertWhenDone(callback){
  // do some work
  callback(); // invoke the callback right before exiting
}

alertWhenDone(function(){
  alert("I am done!"); 
});

// Callback making use of the JavaScript Timer
setTimeout(function(){
  alert("3 seconds have passed.");
}, 3000);
```

<a name="object-oriented"></a>
## 5. Object-Oriented JS and Prototypal Inheritance 

<a name="constructors"></a>
### i. Function Constructors 
When you call a function with the `new` keyword, a new object is created in memory, and is made available to the function via the `this` keyword. Functions designed to be called like that are called constructors.
```javascript
var MyConstructor = function(){
    // public variables are declared using this
    this.myNumber = 5;
    // private variables are declared using var
    var secretNum = 4;
    // public getter for the private variable
    this.getSecret = function(){ return secretNum };
}
myNewObj = new MyConstructor(); // = {myNumber: 5, secretNum: 4}
myNewObj.myNumber; // = 5
myNewObj.secretNum; // undefined
myNewObj.getSecret(); // = 4

```

<a name="prototypes"></a>
### ii. Prototypes  
Every JavaScript object has a 'prototype' property, which is simply a reference to another object. When you go to access a property that doesn't exist on the actual object, the interpreter will look at its prototype. If it doesn't exist on the prototype, it'll look at the prototype's prototype. It will keep looking down this __prototype chain__ until it hits the base object Object, which doesn't have a prototype. 
```javascript
// Some JS implementations let you access an object's prototype on the magic
// property `__proto__`. While this is useful for explaining prototypes it's not
// part of the standard; we'll get to standard ways of using prototypes later.
var myObj = {
    myString: "Hello world!"
};
var myPrototype = {
    meaningOfLife: 42,
    myFunc: function(){
        return this.myString.toLowerCase()
    }
};

myObj.__proto__ = myPrototype;
myObj.meaningOfLife; // = 42

// This works for functions, too.
myObj.myFunc(); // = "hello world!"

// Of course, if your property isn't on your prototype, the prototype's
// prototype is searched, and so on.
myPrototype.__proto__ = {
    myBoolean: true
};
myObj.myBoolean; // = true

// There's no copying involved here; each object stores a reference to its
// prototype. This means we can alter the prototype and our changes will be
// reflected everywhere.
myPrototype.meaningOfLife = 43;
myObj.meaningOfLife; // = 43
```

<a name="prototypal-inheritance"></a>
### iii. Prototypal Inheritance aka setting prototypes of new objects 

Accessing `__proto__` is non-standard, and there are no standard ways to change the prototype of an existing object. However, there are two ways to create a new object with a given prototype.
```javascript
// The first is Object.create, which is a recent addition to JS, and therefore
// not available in all implementations yet.
var myObj = Object.create(myPrototype);
myObj.meaningOfLife; // = 43
```
Every JS function also has a property called 'prototype'. When used as a normal function, the 'prototype' property is not used. Only when functions are used as constructors with the `new` keyword, the 'prototype' sets the prototype of the object being created.

```javascript
// Constructors have a property called prototype. This is *not* the prototype of
// the constructor function itself; instead, it's the prototype that new objects
// are given when they're created with that constructor and the new keyword.
MyConstructor.prototype = {
    myNumber: 5,
    getMyNumber: function(){
        return this.myNumber;
    }
};
var myNewObj2 = new MyConstructor();
myNewObj2.getMyNumber(); // = 5
myNewObj2.myNumber = 6
myNewObj2.getMyNumber(); // = 6
```

<a name="built-in"> </a>
### iv. Built-In Constructors 
```javascript
// Built-in types like strings and numbers also have constructors that create
// equivalent wrapper objects.
var myNumber = 12;
var myNumberObj = new Number(12);
myNumber == myNumberObj; // = true

// Except, they aren't exactly equivalent.
typeof myNumber; // = 'number'
typeof myNumberObj; // = 'object'
myNumber === myNumberObj; // = false
if (0){
    // This code won't execute, because 0 is falsy.
}
if (new Number(0)){
   // This code will execute, because wrapped numbers are objects, and objects
   // are always truthy.
}

// However, the wrapper objects and the regular builtins share a prototype, so
// you can actually add functionality to a string, for instance.
String.prototype.firstCharacter = function(){
    return this.charAt(0);
}
"abc".firstCharacter(); // = "a"
```
__Polyfilling__ takes advantage of the fact that we can modify the built-in prototypes to implement newer features of JavaScript in an older subset of JavaScript, so that they can be used in older environments such as outdated browsers.
```javascript
// For instance, Object.create isn't yet available in all
// implementations, but we can still use it with this polyfill:
if (Object.create === undefined){ // don't overwrite it if it exists
    Object.create = function(proto){
        // make a temporary constructor with the right prototype
        var Constructor = function(){};
        Constructor.prototype = proto;
        // then use it to create a new, appropriately-prototyped object
        return new Constructor();
    }
}

```

<a name="bugs"> </a>
## 6. Bugs and Error Handling 

```javascript
// You can opt in to tell the JS engine to be very strict in its interpretation
// It must go at the top of the file to interpret the whole file in strict mode
// Or at the top of a function, to make just that function strict
"use strict"
```


<a name="es6"></a>
## 7. New ES6 stuff 

### Arrows 
Arrows are a function shorthands for anonymous functions used with the `=>` syntax. They pass the outside lexical scope (ie. `this`) to the function.
```javascript
// Expression bodies
var odds = evens.map(v => v + 1);
var nums = evens.map((v, i) => v + i);

// Statement bodies
nums.forEach(v => {
  if (v % 5 === 0)
    fives.push(v);
});

// Lexical this
var bob = {
  _name: "Bob",
  _friends: [],
  printFriends() {
    this._friends.forEach(f =>
      console.log(this._name + " knows " + f));
  }
}
```

### Classes 
Object-oriented syntactic sugar for the prototypal inheritance pattern.

``` javascript
class SkinnedMesh extends THREE.Mesh {
  constructor(geometry, materials) {
    super(geometry, materials);

    this.idMatrix = SkinnedMesh.defaultMatrix();
    this.bones = [];
    this.boneMatrices = [];
    //...
  }
  update(camera) {
    //...
    super.update();
  }
  get boneCount() {
    return this.bones.length;
  }
  set matrixType(matrixType) {
    this.idMatrix = SkinnedMesh[matrixType]();
  }
  static defaultMatrix() {
    return new THREE.Matrix4();
  }
}
```

### String Interpolation 
``` javascript
var name = "Bob", time = "today";
`Hello ${name}, how are you ${time}?`
```

### `let` and `const` 
`let` is like `var` except it is block-scoped. Variables declared with `const` can only be assigned once.
``` javascript
if (1 < 2) {
  let i = 4;
  const name = 'Jon Snow'
}
var i = 5; // error, i is already defined
name = 'Samwell Tarly' // error, const can only be defined once
```

### Generator 
Functions that can be paused using the `yield` keyword and restarted from the outside. `yield _____` is called a "yield expression" which gets evaluated with whatever value we send in when we restart the generator. `yield` is making a request for a value.

``` javascript
function* fibonacci() {
  let a = 0, b = 1;

  while(true) {
    yield a;
    [a, b] = [b, a + b];
  }
}

// Enumerates the Fibonacci numbers
for(let value of fibonacci()) {
  console.log(value);
}
```
Generators are useful because they return (i.e. create) iterators. In turn, an iterator, an object with a `next` method, actually executes the body of generators. The `next` method, when repeatedly called, partially executes the corresponding generator, gradually advancing through the body until a `yield` keyword is hit.

``` javascript
function* argumentsGenerator() {
  for (let i = 0; i < arguments.length; i += 1) {
    yield arguments[i];
  }
}

var argumentsIterator = argumentsGenerator('a', 'b', 'c');

// Prints "a b c"
console.log(
    argumentsIterator.next().value,
    argumentsIterator.next().value,
    argumentsIterator.next().value
);

// ES6 has syntactic sugar for iteration.
// Prints "a", "b", "c"
for(let value of argumentsIterator) {
  console.log(value);
}
```
The `next` method of an iterator returns an object with a `value` property and a `done` property, as long as the body of the corresponding generator has not `return`ed. The `value` property refers the value `yield`ed or `return`ed. The `done` property is `false` up until the generator body `return`s, at which point it is `true`. If the `next` method is called after `done` is `true`, an error is thrown.

### Maps, Sets, WeakMap, WeakSet 

A Map is an object for which the keys can be any arbitrary object. A Set is a data structure which contains a finite set of elements, each occurring only once. WeakMaps and WeakSets provide leak-free object-key’d side tables. The JavaScript virtual machine periodically frees memory allocated to objects no longer in scope. An object is no longer in scope if there is no chain of references from the current scope leading to it.
``` javascript
// Sets
var s = new Set();
s.add("hello").add("goodbye").add("hello");
s.size === 2;
s.has("hello") === true;

// Maps
var m = new Map();
m.set("hello", 42);
m.set(s, 34);
m.get(s) == 34;

// Weak Maps
var wm = new WeakMap();
wm.set(s, { extra: 42 });
wm.size === undefined

// Weak Sets
var ws = new WeakSet();
ws.add({ data: 42 });
// Because the added object has no other references, it will not be held in the set
```

### Promises 

Promises are a library for asynchronous programming. Promises are a first class representation of a value that may be made available in the future. A Promise is in one of these states:
- pending: initial state, not fulfilled or rejected.
- fulfilled: successful operation
- rejected: failed operation.
- settled: the Promise is either fulfilled or rejected, but not pending.

``` javascript
var someAsyncThing = function() {
  return new Promise(function(resolve, reject) {
    // this will throw, x does not exist
    resolve(x + 2);
  });
};

someAsyncThing().then(function() {
  console.log('everything is great');
}).catch(function(error) {
  console.log('oh no', error);
});
```

### Modules 

``` javascript
// lib/math.js
export function sum(x, y) {
  return x + y;
}
export var pi = 3.141593;
```
```javascript
// app.js
import * as math from "lib/math";
alert("2π = " + math.sum(math.pi, math.pi));
```
```javascript
// otherApp.js
import {sum, pi} from "lib/math";
alert("2π = " + sum(pi, pi));
```

### Proxy

Proxy object is used to define custom behavior for fundamental operations (e.g. property lookup, assignment, enumeration, function invocation, etc).

```javascript
// lib/proxy.js
export function create(target) {
  var target = {};
  return new Proxy(target, {});
}
```

```javascript
// app.js
import * as proxy from 'lib/proxy';
var target = {};
var origin = proxy.create(target);
origin.a = 37; // operation forwarded to the target
alert('target.a = ' + target.a); // The operation has been properly forwarded
```
TODO: Symbol
