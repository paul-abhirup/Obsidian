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


## 03. Objects
```js
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

## 07.  Class 
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

