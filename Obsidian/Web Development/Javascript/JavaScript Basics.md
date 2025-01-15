#js #javascript #webDevelopment

## 01. Strings
```js

str.replace(target, replacement)

str.split(separator)
//splits the string from the seperator
/*
splitString("HelloWWorld", "W");
After split: [ 'Hello', '', 'orld' ]
*/


str.IndexOf(target)  
//we need 2 argument : str , target 
// target may be a word or a letter as both are : string

str.lastIndexOf(target)
//ex -- findIndexOf("Hello World World", "World") = 12

str.slice(start,end)
//slices thr str and serves the slice 

str.substring(start, end) 
//similar to slice function

```


```js
// String: length, indexOf(), lastIndexOf(), slice(), substring(), replace(),split(), trim(), toUpperCase(), toLowerCase(), etc.


// Length
function getLength(str) {
  console.log("Length:", str.length);
}
getLength("Hello World");


// indexOf
function findIndexOf(str, target) {
  console.log("Index:", str.indexOf(target));
}
findIndexOf("Hello World", "World");
//even the whole word is being counted as a letter due to string


// lastIndexOf
function findLastIndexOf(str, target) {
  console.log("Index:", str.lastIndexOf(target));
}
findLastIndexOf("Hello World World", "World");
//if index is -1

// slice
function getSlice(str, start, end) {
  console.log("After slice:", str.slice(start, end));
}
getSlice("Hello World", 0, 5);
getSlice("Hello World", 0, -1);//is like 1 element from the last position
getSlice("Hello World", 0, 0);//returns nothing 

// substring
function getSubstring(str, start, end) {
  console.log("After substring:", str.substring(start, end));
}
getSubstring("Hello World", 0, 5);

// replace
function replaceString(str, target, replacement) {
  console.log("After replace:", str.replace(target, replacement));
}
replaceString("Hello World", "World", "JavaScript");

// split
function splitString(str, separator) {
  console.log("After split:", str.split(separator));
}
splitString("Hello World", " ");

// trim
function trimString(str) {
  console.log("After trim:", str.trim());
}
trimString(" Hello World ");

// toUpperCase
function toUpper(str) {
  console.log("After toUpperCase:", str.toUpperCase());
}
toUpper("Hello World");

// toLowerCase
function toLower(str) {
  console.log("After toLowerCase:", str.toLowerCase());
}
toLower("Hello World");

//join


```
#### slice vs string
**What they have in common:**

1. If `start` equals `stop`: returns an empty string
2. If `stop` is omitted: extracts characters to the end of the string
3. If either argument is greater than the string's length, the string's length will be used instead.

**Distinctions of** [`substring()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/substring)**:**

1. If `start > stop`, then `substring` will swap those 2 arguments.
2. If either argument is negative or is `NaN`, it is treated as if it were `0`.

**Distinctions of** [`slice()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/slice)**:**

1. If `start > stop`, `slice()` will return the empty string. (`""`)
2. If `start` is negative: sets char from the end of string, exactly like `substr()` in Firefox. This behavior is observed in both Firefox and IE.
3. If `stop` is negative: sets stop to: `string.length – Math.abs(stop)` (original value), except bounded at 0 (thus, `Math.max(0, string.length + stop)`) as covered in the [ECMA specification](https://www.ecma-international.org/ecma-262/9.0/index.html#sec-string.prototype.slice).


## 02. Arrays

In majority lang like c,c++, etc arrays are homogenous in nature
*unlike in js, Arrays can contain any datatypes -- heterogenous*

```jsx

// Array Methods  
// push(), pop(), shift(), unshift(), splice(), slice(), concat(), forEach(), map(), filter(), reduce(), find(), sort()

// push()
function pushExample(arr, element) {
  arr.push(element);
  console.log("After push:", arr);
}
pushExample([1, 2, 3], 4);


// pop()
function popExample(arr) {
  arr.pop();
  console.log("After pop:", arr);
}
popExample([1, 2, 3]);



// shift()
function shiftExample(arr) {
  arr.shift();
  console.log("After shift:", arr);
}
shiftExample([1, 2, 3]);



// unshift()
function unshiftExample(arr, element) {
  arr.unshift(element);
  console.log("After unshift:", arr);
}
unshiftExample([1, 2, 3], 0);



// concat()
function concatExample(arr1, arr2) {
  let arr3 = arr1.concat(arr2);
  console.log("After concat:", arr3);
}
concatExample([1, 2, 3], [4, 5, 6]);



// forEach()
function forEachExample(arr) {
  arr.forEach(function(item, index) {
    console.log(item, index);
  });
}
forEachExample([1, 2, 3]);



// map()
function mapExample(arr) {
  let newArr = arr.map(function(item) {
    return item * 2;
  });
  console.log("After map:", newArr);
}
mapExample([1, 2, 3]);



// filter()
function filterExample(arr) {
  let newArr = arr.filter(function(item) {
    return item > 3;
  });
  console.log("After filter:", newArr);
}
filterExample([1, 2, 3, 4, 5]);



// find()
function findExample(arr) {
  let found = arr.find(function(item) {
    return item > 3;
  });
  console.log("After find:", found);
}
findExample([1, 2, 3, 4, 5]);



// sort()
function sortExample(arr) {
  arr.sort(function(a, b) {
    return a - b;
  });
  console.log("After sort:", arr);
}
sortExample([5, 2, 3, 4, 1]);

```

Higher Order Methods for Array
```js
const students = ["Piyush", "Abhi", "king"]

//.forEach()
students.forEach((val) => console.log(val + " garg"));
// takes every element of the array each time, and then performs the function upon it 

//output
Piyush garg
Abhi garg
king garg

//.map()
students.map((val) => console.log(val + "garg"));

// difference between both the methods ----
// map returns an new array in the output, while manipulating the array
//whereas foreEach just loops on the prev array, returns nothing


// find 
let ans = students.find((val) => val === "king");
console.log(ans); //find the element of the array

// findIndex
let ans = students.findIndex((val) => val === "king");
//finds the index of the element


const numbers = [1,2,3,4,5,6,7,8,9]

//filter 
const newArr = numbers.filter((num) => num % 2);
// reutrns an array with only even no in it

//slice
const newArr = numbers.slice(1,6);
//3,4,5,6
// cuts the array in between this components

//splice
const newArr = numbers.splice(1,4);
// cuts the array from index 1 to next 4 elements

console.log(newArr);
console.log(numbers);

```

## DOM

chrome dev tools -- 
- elements -- shows the html code of the site 
	- styles, layouts, etc
- console -- related to js 
- application -- 
	- localstorage , session storage, cookies,etc

```js
alert("hi!");//for notification

prompt("what is your name?");// takes input from the user

window --- // window related to the browser
//any interaction we do with the browser is related to this window object by default
// window.console.log() => console.log();
// window.alert() => alert();

document ---// ur code 
// we use this to interact with the DOM aka ur code 
// example --
// in ur html code // title = "next site"

window.document.title 
//aka
document.title = "Paul's site" 
// this changes the title from next site to Paul's site 

```

#### HTML code
for the understandding of the DOM
```js
<!DOCTYPE html>
<html>
  <head>
    <title>DOM!</title>
    <link rel="stylesheet" href="styles.css" />
  </head>
  <body>
    <nav class="block">
      <p class="paragraph"> Welcome to my website</p>
    </nav>
    <div class="block">
      <h4>Hi I am <span id="username">Abhirup</span></h4>
      <p class="paragraph">Here is a code for you</p>
      <pre><code>console.log("Hello World")</code></pre>
    </div>
      <script>
        // All js manipulations will be done here
      </script>
  </body>
</html>
```
### Query Selectors
```js

```

### Select Element by id
```js

```

### Get element by classname
```js

```

### Event Listeners
```js

```

## 03. Objects
```js
//oblect declaration
const person = {
	firstname: "piyush",
	lastname: "garg",
	age: "27",
	subject: "CSE",
	mettha: true
}


// Object Methods Explanation
function objectMethods(obj) {
  console.log("Original Object:", obj);

  let keys = Object.keys(obj);
  console.log("After Object.keys():", keys);

  let values = Object.values(obj);
  console.log("After Object.values():", values);

  let entries = Object.entries(obj);
  console.log("After Object.entries():", entries);

  let hasProp = obj.hasOwnProperty("property");
  console.log("After hasOwnProperty():", hasProp);

  let newObj = Object.assign({}, obj, { newProperty: "newValue" });
  console.log("After Object.assign():", newObj);


}

// Example Usage for Object Methods
const sampleObject = {
  key1: "value1",
  key2: "value2",
  key3: "value3",
};

objectMethods(sampleObject);

```


## 04. JSON
```js

function jsonMethods(jsonString) {
  console.log("Original JSON String:", jsonString);

  // Parsing JSON string to JavaScript object
  let parsedObject = JSON.parse(jsonString);
  console.log("After JSON.parse():", parsedObject);

  // Stringifying JavaScript object to JSON string
  let jsonStringified = JSON.stringify(parsedObject);
  console.log("After JSON.stringify():", jsonStringified);
}

// Example Usage for JSON Methods
const sampleJSONString =
  '{"key": "value", "number": 42, "nested": {"nestedKey": "nestedValue"}}';

jsonMethods(sampleJSONString);

```


## 05. Maths, numbers
```js
//Numbers

function explainParseInt(value) {
  console.log("Original Value:", value);
  let result = parseInt(value);
  console.log("After parseInt:", result);
}

// Example Usage for parseInt
explainParseInt("42");
explainParseInt("42px");
//any no other than int will be ignored
//like px , .14 
explainParseInt("3.14");

function explainParseFloat(value) {
  console.log("Original Value:", value);
  let result = parseFloat(value);
  console.log("After parseFloat:", result);
}

// Example Usage for parseFloat
explainParseFloat("3.14");
explainParseFloat("3.148768678");
explainParseFloat("42");
explainParseFloat("42px");
//only charachters will be ignored

```

```js
//Math Functions

function mathMethods(value) {
  console.log("Original Value:", value);

  let rounded = Math.round(value);
  console.log("After round():", rounded);

  let ceiling = Math.ceil(value);
  console.log("After ceil():", ceiling);

  let flooring = Math.floor(value);
  console.log("After floor():", flooring);

  let randomValue = Math.random();
  console.log("After random():", randomValue);

  let maxValue = Math.max(5, 10, 15);
  console.log("After max():", maxValue);

  let minValue = Math.min(5, 10, 15);
  console.log("After min():", minValue);

  let powerOfTwo = Math.pow(value, 2);
  console.log("After pow():", powerOfTwo);

  let squareRoot = Math.sqrt(value);
  console.log("After sqrt():", squareRoot);
}

// Example Usage for Math Methods
mathMethods(4.56);
mathMethods(9);
mathMethods(25);

```


## 06. Date
```js
//Date funcitons

function dateMethods() {
  const currentDate = new Date();
  console.log("Current Date:", currentDate);

  // Getting various components of the date
  console.log("Date:", currentDate.getDate());
  console.log("Month:", currentDate.getMonth() + 1);
 // Months are zero-indexed, so adding 1
  console.log("Year:", currentDate.getFullYear());
  console.log("Hours:", currentDate.getHours());
  console.log("Minutes:", currentDate.getMinutes());
  console.log("Seconds:", currentDate.getSeconds());

  // Setting components of the date
  currentDate.setFullYear(2022);
  console.log("After setFullYear:", currentDate);

  currentDate.setMonth(5); // Setting month to June (zero-indexed)
  console.log("After setMonth:", currentDate);

  // Getting and setting time in milliseconds since 1970
  console.log("Time in milliseconds since 1970:", currentDate.getTime());
  // epoch timestamp


  const newDate = new Date(2023, 8, 15); // Creating a new date
  console.log("New Date:", newDate);
}

// Example Usage for Date Methods
dateMethods();


```

## 07. Class 
#### Classes

In JavaScript, classes are a way to define blueprints for creating objects (these objects are different from the objects datatype).

```js
class Rectangle {
   constructor(width, height, color) {
	    this.width = width;
	    this.height = height;
	    this.color = color; 
   }
   
   area() {
	   const area = this.width * this.height;
		 return area;
   }
   
   paint() {
			console.log(`Painting with color ${this.color}`);
   }
   
}

const rect = new Rectangle(2, 4);
const area = rect.area();
console.log(area)
```

Key Concepts
- Class Declaration:
	- Inside a class, you define properties (variables) and methods (functions) that will belong to the objects created from this class.
- Constructor:
	- A special method inside the class that is called when you create an instance (an object) of the class.
	- It’s used to initialize the properties of the object.
- Methods:
	- Functions that are defined inside the class and can be used by all instances of the class.
- Inheritance:
	- Classes can inherit properties and methods from other classes, allowing you to create a new class based on an existing one.
- Static Methods:
	- Methods that belong to the class itself, not to instances of the class. You call them directly on the class.
- Getters and Setters:
	- Special methods that allow you to define how properties are accessed and modified.
- new Keyword
	-  The new keyword creates a new empty object(instance), with a type of object.
	- The new keyword sets the internal prototype property of the constructing function.
	- The new keyword binds this variable to the newly created object and returns it .

### Inheritance in classes

Inheritance in JavaScript classes allows one class to inherit properties and methods from another class. 

Creating a Base Class
```js
class Shape {
    constructor(color) {
        this.color = color;
    }

    paint() {
			console.log(`Painting with color ${this.color}`);
    }

    area() {
        throw new Error('The area method must be implemented in the subclass');
    }

    getDescription() {
        return `A shape with color ${this.color}`;
    }
}
```

Creating a Rectangle Class from Base class; with additonal properties
```js
class Rectangle extends Shape {
    constructor(width, height, color) {
        super(color);  // Call the parent class constructor to set the color
        this.width = width;
        this.height = height;
    }

    area() {
        return this.width * this.height;
    }

    getDescription() {
        return `A rectangle with width ${this.width}, height ${this.height}, and color ${this.color}`;
    }
}
```

Calling rectangle class
```js
const Rectangle1 = new Rectangle(10,20,"red");
console.log(Rectangle1.area());
console.log(Rectangle1.paint());
console.log(Rectangle1.getDescription());
```


## 08. Functions in JS
```javascript

// Logical operators
/*
AND  &&
OR   ||
NOT  !
*/

// let a = 1000;
// if (!(a > 10 || a < 100)){
//   console.log("done")
// }else {
//   console.log("lol")
// }

```

# 8.1 Functions
```js
////// FUNCTIONS

//Anonymous Function 
//nameless function 
function(a){
return a*a;
}
 
// accessing unlimited arguments
//arguments keyword 
// The arguments object is a local variable available within all non-arrow functions.

function printer(){
  console.log(arguments);
}
printer(34,34,33,33,222,444,33);
//Output
[Arguments] {
  '0': 34,
  '1': 34,
  '2': 33,
  '3': 33,
  '4': 222,
  '5': 444,
  '6': 33
}

function sum(){
  let ans = 0;
  for(i=0;i< arguments.length;i++){
    ans = ans + arguments[i];
  }
  // return ans;
  console.log(ans)
}
// console.log(sum(12, 23, 34, 45, 45, 56, 56, 67, 76))
sum(12, 23, 34, 45, 45, 56, 56, 67, 76);


//spread operator
//taking array as an input
function sum(...numbers){
  let ans = 0;
  for(i=0;i<numbers.length;i++){
    ans = ans + numbers[i];
  }
  return ans;
}
let result = sum(12, 23, 34, 45, 45, 56, 56, 67, 76);
console.log(result);

```


# 8.2 Composition in JS
Composing multiple functions in JS 
```jsx

function add(a, b) {
  return a + b;
}
function square(val) {
  return val * val;
}
function multiply(args) {
  return args[0] * args[1];
}
// function addAndSquare(a, b) {
//   return square(add(2, 3));
// }

// const addResult = add(2, 3);
// console.log(square(addResult));

// console.log(addAndSquare);

// generic compose function syntax //
// function composeTwoFunction(fn1, fn2) {
//   return function (a, b) {
//     return fn2(fn1(a, b));
//   };
// }

// // using modern js
// const c2f = (fn1, fn2) => (a, b) => fn2(fn1(a, b));

// //example
// const task = c2f(add, square);
// console.log(task(2, 3));

//for composing unlimited fns
function compose(...fns) {
  return function (...value) {
    return fns.reduce((a, b) => b(a), value);
  };
}

const composeAll =
  (...fns) =>
  (...val) =>
    fns.reduce((a, b) => b(a), val);

// const task = composeAll(add, square, (val) => val + 10);//NaN
const task = composeAll(multiply, square, (val) => val + 10); //46

console.log(task(2, 3));
```

# 8.3 Closer
```jsx
function main() {
  const name = "Paul";
  function sayMyName() {
    console.log(name);
  }
  sayMyName();
}
main();
```

# 8.4 Arrow functions
``` jsx
/*
 * ARROW FUNCTIONS
 */

1. syntax
//normal function 

function sum(a,b){
  let ans = a + b ;
  return ans;
}
sum(1,2);

const sum = (a,b) => {
  let ans = a + b;
  return ans;
}
console.log(sum(2,3));



//here u have to use return if u have used {}
const add = (a,b) => {
  return a + b;
}

//u can ommit return by using one Liner
const addV2 = (a,b) => a+b ; // one-liner


//=============================================================


2. 'arguments' keyword

/// not works on arrow function 
// arguments is not defined in arrow function 

 const addNumbers = () => {
   console.log(arguments);
 }
 addNumbers(1,2,3);


//using spread operator
//to access array of arguments

 const addNumbers = (...nums) => {
   console.log(nums)
 }
 addNumbers(1,2,4);

//spread operator will not cause an issue with function arguments understanding because the arguments of a function is different for every function 
//also the function name is different because u cant create 2 functions with same name in js // function overload //
// also if u have same function with 2 different arguments the function will be called 2 times with diferent arguments 
//example ----------

 const addNumbers = (...nums) => {
   console.log(nums);
 }
 addNumbers(1, 2, 3, 4, 5, 5, 6)
 addNumbers(1, 32);

//output for this is 

// [ 1, 2, 3, 4, 5, 5, 6 ]
// [1, 32]



//=================================================================
  

3. Hoisting

// in hoisting the sequence of code dont matter

// Hoisting // is a JavaScript mechanism that moves all variable and function declarations to the top of their scope before code execution. This means that variables and functions can be used before they are declared.

//for a normal function


// case 1
sayHi();
function sayHi(){
console.log("hi");
}


// case 2
function sayHi(){
console.log("hi");
}
sayHi();
 

//In arrow function
const sayHi = () => {
console.log("hi");
}
sayHi();
 

//=======================================================

4. This Keyword
const obj = {
  value: 20,
  myFunction: function () {
    console.log("the value is "+ this.value);
  },  
};
obj.myFunction();
// output//
// the value is 20

// in normal function this keyword reffers to the object aka the caller function 
// here this refers to the object 

const obj = {
  value: 20,
  myFunction: () => {
    console.log("the value is " + this);
  },
};
obj.myFunction();
// output//
// the value is[object Object]

// arrow function is of global scope so, the 'this' keyword reffers to the window object ,i.e, the browser
//window object is the global object

/*
arrow function dont have their own this keyword
they inherit the this keyword from the parent scope
here the parent scope is the global scope
so the this keyword reffers to the global scope  
*/

```


# 8.5 Higher Order Functions
```jsx

//Higher order function and callbacks


//function that call a function in argument is called higher order function
//function that gets called in argument is called callback

function add(a, b, cb) {
  let result = a + b;
  cb(result);
}
add(2, 3, (val) => console.log(val))  //this arriow function defines the cb function
add(2, 3, val => console.log(val)) //js automatically put 1st brackets on val

function add(a, b, cb) {
  let result = a + b;
  cb(result);
  return () => console.log(result);
}

add(3,4, () => {});//this dont work

let resultFunction = add(3, 4, () => { });
resultFunction();

//=====================================================

/**
 *  ///Arrays
 * 
 * heterogenous in nature
 *   // in Js u can have strings, emojis , numbers , etc all in one array
 *  //  -1 means the value dont exist in the array
 *   
 */


//Array methods 
// .push(), .pop(), .idexOf(), 
// .reverse() //this reverse the whole array

const students = ["Piyush", "ram", "sam", "k"]
console.log(students.length); // length of an array 
students[0] // accessing the element of the array 

// u cant reinitalize students array but obviously can change the array 
students = ["1"]; //errror

students.push("alexa") // pushes element in the end of the array
students.pop("alexa") // pops out element in the end of the array
students.reverse();  //reverse the whole array

```

# 8.6 Scope, Lexical Scope, Curry

Scope --> area where an item(func, variable) can be accesible
- Global Scope --> available globally, can be used locally
- Local Scope --> available locally only, cant be used globally

#### Scope Chain
```js
const f1 = "mclaren";
function f2(){
  function f3(){
    function f4(){
      return f1;
    }
    return f4();
  }
  return f3();
}

//calling f2();
f2();
```
lexical scope -->means "origin" 
#### Working of Lexical Chain
- How Scope Chain works ?
- finding lexical scope("origin") on f1 

In JS 
1) Js will check if f1 is defined locally within f4( ), if not it will move up the chain
2) check if f1 is in f3( ), if not move up the chain 
3) similarly check if f1 is in f2()
4) last check for gobal scope
5) in case, not find, JS returns "reference Error"

#### Lexical Scope in JS (alias, static scope)

lexical -> meaning creating words, expressions or variables
In dicationary -->alias "lexicon"

The place where an item is defined (item's defination space)/Origin
"defination space "  not " in"
Lexical environment --> Surrounding Space 

# 8.7 Curry in Js
```js
// normal func
function add(a,b,c){
  return a+b+c;
}

//calling function
add(1,2,3);

//Curry
function add(a){
  return function(b){
    return function(c){
      return a+b+c;
    }
  }
}
add(2)(3)(5); //10
add(2)(3) //Error
//3 parameters are mandatory

//Using ES6 
const add = (a) => (b) => (c) => a+b+c;

```


# 8.8 Async Await Promise

**I/O (Input/Output) heavy operations** refer to tasks in a computer program that involve a lot of data transfer between the program and external systems or devices. These operations usually require waiting for data to be read from or written to sources like disks, networks, databases, or other external devices, which can be time-consuming compared to in-memory computations.

Examples --
- reading a file 
- HTTP requests
- starting a clock

`require` statement lets you import code/functions export from another file/module.

I/O-bound tasks are operations that are limited by the system’s input/output capabilities, such as disk I/O, network I/O, or any other form of data transfer. These tasks spend most of their time waiting for I/O operations to complete
```js
const fs = require("fs");

const contents = fs.readFileSync("a.txt", "utf-8");
console.log(contents);

const contents2 = fs.readFileSync("b.txt", "utf-8");
console.log(contents2);

```
synchronous, so it takes a lot of time to be done

CPU-bound tasks are operations that are limited by the speed and power of the CPU. These tasks require significant computation and processing power, meaning that the performance bottleneck is the CPU itself.
```c++
let ans = 0;
for (let i = 1; i <= 1000000; i++) {
	ans = ans + i
}
console.log(ans);	
```

- One by one (sync-hronously)
- Context switch between them (Concurrently)
- Start all 3 tasks together, and wait for them to finish. The first one that finishes gets catered to first (async-hronously)

read from a file 
```js
const fs = require("fs");

fs.readFile("a.txt", "utf-8", function (err, contents) {
  console.log(contents);
});
```

seTimeout 
```js
function run() {
	console.log("I will run after 1s");
}

setTimeout(run, 1000);
console.log("I will run immedietely");
```


### JS Architechture for Async
How JS executes asynchronous code - [http://latentflip.com/loupe/](http://latentflip.com/loupe/)
```js
function first() {
  console.log("First");
}
function second() {
  first();
  console.log("Second");
}
second();
```

1. Call Stack
 The call stack is a data structure that keeps track of the function calls in your program. It operates in a "Last In, First Out" (LIFO) manner, meaning the last function that was called is the first one to be executed and removed from the stack.
- When a function is called, it gets pushed onto the call stack. When the function completes, it's popped off the stack.

2. Web APIs
- Web APIs are provided by the browser (or the Node.js runtime) and allow you to perform tasks that are outside the scope of the JavaScript language itself, such as making network requests, setting timers, or handling DOM events.

3. Callback Queue 
- The callback queue is a list of tasks (callbacks) that are waiting to be executed once the call stack is empty. These tasks are added to the queue by Web APIs after they have completed their operation.

4. Event loop
- The event loop constantly checks if the call stack is empty. If it is, and there are callbacks in the callback queue, it will push the first callback from the queue onto the call stack for execution.


#### Async vs Sync 
sync works in a step by step manner 
async works in a multitasking manner 

```jsx
// async func
console.log("I");

setTimeout(()=>{
console.log("kiara");
}, 3000);

console.log("love");
```

```jsx
//callback

//f1
let l1 = (wth) => {
    console.log("i love kiara ");
    wth();
}

//f2
let l2 = () => {
    console.log("kiara loves me");
}

//trigger
l1(l2);

```


#### Callback Hell  aka "nested callback"
when callbacks are nested one over the other 
issue -
- difficult to debug 
- not clean 
So, we use promises to deal with them 
```jsx
//classical structure of callback hell
let production = () =>{

  setTimeout(()=>{
    console.log("production has started")
    setTimeout(()=>{
      console.log("The fruit has been chopped")
      setTimeout(()=>{
        console.log(`${stocks.liquid[0]} added`)
        setTimeout(()=>{
          console.log("start the machine")
          setTimeout(()=>{
            console.log(`Ice cream placed on`)
            setTimeout(()=>{
              console.log(`${stocks.toppings[0]} as toppings`)
              setTimeout(()=>{
                console.log("serve Ice cream")
              },2000)
            },3000)
          },2000)
        },1000)
      },1000)
    },2000)
  },0000)

};
```


### Things to keep in mind

1. You can only call `await` inside a function if that function is `async`
2. You cant have a `top level await`
3. its a syntactical sugar that lets you write async code in a sync style
4. Build on top of Promises and allows you to avoid chaining `.then()` and `.catch()` methods while still working with asynchronous operations.

```js

//Q: Write code that
//logs hi after 1 second
//logs hello 3 seconds after step 1
//logs hello there 5 seconds after step 2

///////////////////////////////////////////////////
//using Promise
///////////////////////////////////////////////////
function setTimeoutPromisified(ms) {
  return new Promise((resolve) => setTimeout(resolve, ms));
}

setTimeoutPromisified(1000)
  .then(function () {
    console.log("hi");
    return setTimeoutPromisified(3000);
  })
  .then(function () {
    console.log("hello");
    return setTimeoutPromisified(5000);
  })
  .then(function () {
    console.log("hello there");
  });


///////////////////////////////////////////////////
//using Async Await 
///////////////////////////////////////////////////
function  setTimeoutPromisified(ms) {
  return new Promise((resolve) => setTimeout(resolve, ms));
}

async function Solve(){
await setTimeoutPromisified(1000);
    console.log("hi");
await setTimeoutPromisified(3000);
    console.log("hello");
await setTimeoutPromisified(5000);
    console.log("hello there");
}

Solve();

```



```js
Write async funct that takes 
- reads contents of a file 
- trims the extra spaces from left and right 
- write it back to the file 


//callback approach 
const fs = require("fs");
function cleanFile(filePath, cb) {
  fs.readFile(filePath, "utf-8", function (err, data) {
    data = data.trim();
    fs.writeFile(filePath, data, function () {
      cb();
    });
  });
}

function onDone() {
  console.log("file has been cleaned");
}
cleanFile("a.txt", onDone);

///////////////////////////////////////////////////

//promises
const fs = require("fs");
function cleanFile(filePath, cb) {
  return new Promise(function (resolve) {
    fs.readFile(filePath, "utf-8", function (err, data) {
      data = data.trim();
      fs.writeFile(filePath, data, function () {
        resolve();
      });
    });
  });
}

async function main() {
  await cleanFile("a.txt");
  console.log("Done cleaning file");
}

main();

```


### Promise class
 
A Promise in JavaScript is an object that represents the eventual completion (or failure) of an asynchronous operation and its resulting value. Promises are used to handle asynchronous operations more effectively than traditional callback functions, providing a cleaner and more manageable way to deal with code that executes asynchronously, such as API calls, file I/O, or timers.

- promises makes relationships between parent, child, grandchild ,.....
- promises are easy to call, hard to define

 Using a function that returns a promise
```js
//Calling is easy, defining is hard
function setTimeoutPromisified(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

function callback() {
	console.log("3 seconds have passed");
}

//using promisification
setTimeoutPromisified(3000).then(callback)

//using callbacks
setTimeout(callback, 3000);
```


```jsx
// Promise cycle
// Promise, promise chanining, .then, .catch, .finally
let stocks = {
    Fruits : ["strawberry", "grapes", "banana", "apple"],
    liquid : ["water", "ice"],
    holder : ["cone", "cup", "stick"],
    toppings : ["chocolate", "peanuts"],
 };

let is_shop_open = true;
//this tells about the shop open or closed 
// if its open we are serving ice cream and vice versa

let order = (time,work) => {
    return new Promise( (resolve, reject) =>{
        if(is_shop_open){
            // resolve(work());
            setTimeout(() => {
                resolve(work());
            }, time );
        }else {
            reject(console.log("we are closed "));
        }
    })
}

//trigger fn
//order(1500, () => console.log(`${stocks.Fruits[0]} was selected`));
//1500 takes 1500 sec

//promise chaining (.then ...... .then ) part

    step 1
    order(2000,()=>console.log(`${stocks.Fruits[0]} was selected`))

    // step 2
    .then(()=>{
      return order(0,()=>console.log('production has started'))
    })

    // step 3
    .then(()=>{
      return order(2000, ()=>console.log("Fruit has been chopped"))
    })

    // step 4
    .then(()=>{
      return order(1000, ()=>console.log(`${stocks.liquid[0]} and ${stocks.liquid[1]} added`))
    })

    // step 5
    .then(()=>{
      return order(1000, ()=>console.log("start the machine"))
    })

    // step 6
    .then(()=>{
      return order(2000, ()=>console.log(`ice cream placed on ${stocks.holder[1]}`))
    })

    // step 7
    .then(()=>{
      return order(3000, ()=>console.log(`${stocks.toppings[0]} as toppings`))
    })

    // Step 8
    .then(()=>{
      return order(2000, ()=>console.log("Serve Ice Cream"))
    })


//error handling    
.catch(() => {
    console.log("customer left")
})
//this catch only works when our promise is rejected
//that is we cant serve ice cream to the customer 
// if_shop_open = false 
//then we cant serve ice cream to the customer



.finally(() => {
    console.log("day ended we are closed")
})
//.finally() runs whether the promise is resolved or not(rejected)
//it will run regardless of the outcome

```



```js
//Q: Write code that
//logs hi after 1 second
//logs hello 3 seconds after step 1
//logs hello there 5 seconds after step 2


//using Callback HEll
setTimeout(function () {
  console.log("hi");
  setTimeout(function () {
    console.log("hello");
    setTimeout(function () {
      console.log("hello there");
    }, 5000);
  }, 3000);
}, 1000);


//ALt sol
//without callback hell
function step3Done() {
  console.log("hello there step3");
}
function step2Done() {
  console.log("hello step2");
  setTimeout(step3Done, 5000);
}
function step1Done() {
  console.log("hi step1");
  setTimeout(step2Done, 3000);
}

setTimeout(step1Done, 1000);

```

Now using Promisified version
```js

//Q: Write code that
//logs hi after 1 second
//logs hello 3 seconds after step 1
//logs hello there 5 seconds after step 2

//This has callback hell
function setTimeoutPromisified(ms) {
  return new Promise((resolve) => setTimeout(resolve, ms));
}

setTimeoutPromisified(1000).then(function () {
  console.log("hi");
  setTimeoutPromisified(3000).then(function () {
    console.log("hello");
    setTimeoutPromisified(5000).then(function () {
      console.log("hello there");
    });
  });
});


//Alt sol //elegant
function setTimeoutPromisified(ms) {
  return new Promise((resolve) => setTimeout(resolve, ms));
}

setTimeoutPromisified(1000)
  .then(function () {
    console.log("hi");
    return setTimeoutPromisified(3000);
  })
  .then(function () {
    console.log("hello");
    return setTimeoutPromisified(5000);
  })
  .then(function () {
    console.log("hello there");
  });


```

### err first Callbacks
`fs.readFile` function used an `err first callback` approach to propagate back errors

```javascript
const fs = require("fs")
function afterDone(err, data) {
  if (err) {
    console.log("Error while reading file");
  } else {
    console.log(data)
  }
}

fs.readFile("a.txt", "utf-8", afterDone);
```

### Rejects in Promises
Promises use the `reject` argument to propagate errors

```javascript
const fs = require("fs");

function readFilePromisified(filePath) {
  return new Promise(function (resolve, reject) {
    fs.readFile(filePath, "utf-8", function (err, data) {
      if (err) {
        reject("Error while reading file");
      } else {
        resolve(data);
      }
    });
  });
}

function onDone(data) {
  console.log(data);
}

function onError(err) {
  console.log("Error: " + err);
}

readFilePromisified("a.txt").then(onDone).catch(onError);
```

