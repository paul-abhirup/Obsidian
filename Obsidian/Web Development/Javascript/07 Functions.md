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


```js
////// FUNCTIONS
 
 
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



## Composition in JS
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
