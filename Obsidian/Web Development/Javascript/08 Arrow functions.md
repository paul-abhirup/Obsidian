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