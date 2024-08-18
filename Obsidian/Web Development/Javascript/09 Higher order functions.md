
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
