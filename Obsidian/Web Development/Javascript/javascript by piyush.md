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



/**
 * 
 * ////////FUNCTIONS
 * 
 */
 
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

## Higher order functions 
```jsx

/**
 * Higher order function and callbacks
 * 
 */

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

## Composition
```jsx
//composition

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

# Closer
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
