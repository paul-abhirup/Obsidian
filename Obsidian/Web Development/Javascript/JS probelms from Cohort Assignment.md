#js #javascript 

```js

/*
  Write a function `isAnagram` which takes 2 parameters and returns true/false if those are anagrams or not.
  What's Anagram?
  - A word, phrase, or name formed by re-arranging the letters of another, such as spar, formed from rasp.
*/

function isAnagram(str1, str2) {
  // Convert the strings to lowercase and remove any non-alphabetic characters
  const cleanStr1 = str1.toLowerCase().replace(/[^a-z]/g, '');
  const cleanStr2 = str2.toLowerCase().replace(/[^a-z]/g, '');

  // Sort the characters in the strings
  const sortedStr1 = cleanStr1.split('').sort().join('');
  const sortedStr2 = cleanStr2.split('').sort().join('');

  // Compare the sorted strings
  if(sortedStr1 === sortedStr2){
    console.log("true")
  }else{
    console.log("false")
  }
}

// module.exports = isAnagram;
isAnagram("openai", "aipen");

//explanation ----------------
// replace(/[^a-z]/g, '')
//replace() -- this finds and replace occurances of the pattern wihtin the string
// [] - character set 
// ^ - negation 
// this says that anything that is doesnt belong to any of a-z should be replaced with ''
//g is the global flag

//const str = "Hello, W00rld!";
//const newStr1 = str.replace(/0/g, 'o'); // Replaces all '0' with 'o'
c//onsole.log(newStr1); // Output: "Hello, Woorld!"

//const newStr2 = str.replace(/0/, 'o'); // Replaces only the first '0'
//console.log(newStr2); // Output: "Hello, Wo0rld!"



-----------------------------------------------------------------
/*
  Implement a function `calculateTotalSpentByCategory` which takes a list of transactions as parameter
  and return a list of objects where each object is unique category-wise and has total price spent as its value.
  transactions is an array where each
  Transaction - an object like 
        {
		id: 1,
		price: 10,
		category: 'Food',
		itemName: 'Pizza',
		}
		
  Output - [{ category: 'Food', totalSpent: 10 }] // Can have multiple categories, only one example is mentioned here
*/

function calculateTotalSpentByCategory(transactions) {
  const categories = {};
  transactions.forEach((transaction) => {
    if (!categories[transaction.category]) {
      categories[transaction.category] = 0;
    }
    categories[transaction.category] += transaction.price;
  });
  return Object.keys(categories).map((category) => ({
    category,
    totalSpent: categories[category],
  }));
}
module.exports = calculateTotalSpentByCategory;


-----------------------------------------------------------------
/*
  Write a function `findLargestElement` that takes an array of numbers and returns the largest element.
  Example:
  - Input: [3, 7, 2, 9, 1]
  - Output: 9
*/

function findLargestElement(numbers) {
  const numberSorted = numbers.sort((a, b) => {
    return a - b;
  });
  maxno = Math.max(...numbers);
  console.log(numberSorted, maxno);
}

//Alternate Method

// function findLargestElement(numbers) {
//   let largestElement = numbers[0];
//   for (let i = 1; i < numbers.length; i++) {
//     if (numbers[i] > largestElement) {
//       largestElement = numbers[i];
//     }
//   }
//   return largestElement;
// }

module.exports = findLargestElement;


-----------------------------------------------------------------
/*
  Implement a function `countVowels` that takes a string as an argument and returns the number of vowels in the string.
  Note: Consider both uppercase and lowercase vowels ('a', 'e', 'i', 'o', 'u').

  Once you've implemented the logic, test your code by running
*/

function countVowels(str) {
  const vowels = ["a", "e", "i", "o", "u"];
  let count = 0;
  for (let i = 0; i < str.length; i++) {
    if (vowels.includes(str[i].toLowerCase())){
      count++;
    }
  }
  return count;
}

countVowels("paul");

module.exports = countVowels;


-----------------------------------------------------------------
/*
  Implement a function `isPalindrome` which takes a string as argument and returns true/false as its result.
  Note: the input string is case-insensitive which means 'Nan' is a palindrom as 'N' and 'n' are considered case-insensitive.

*/

function isPalindrome(str) {
  const lowercaseStr = str.toLowerCase();
  const filteredStr = lowercaseStr
    .split("")
    .filter(
      (char) =>
        char !== "?" &&
        char !== " " &&
        char !== "!" &&
        char !== "." &&
        char !== ","
    )
    .join("");
  const reversedStr = filteredStr.split("").reverse().join("");
  return filteredStr === reversedStr;
}

module.exports = isPalindrome;


-----------------------------------------------------------------
/*
Write a function that calculates the time (in seconds) it takes for the JS code to calculate sum from 1 to n, given n as the input.
Try running it for
1. Sum from 1-100
2. Sum from 1-100000
3. Sum from 1-1000000000
Hint - use Date class exposed in JS
There is no automated test for this one, this is more for you to understand time goes up as computation goes up
*/

function calculateTime(n) {
    const startTime = Date.now();
    let sum = 0;
    for(i=0;i<n;i++){
        sum+= i
    }
    const finalTime = Date.now();
    const time = finalTime - startTime ;
    console.log(`${time / 1000} seconds`);

}

calculateTime(100);
calculateTime(10000);
calculateTime(1000000);

//// ------- note ------ // wrong way
// function calculateTime(n) {
//   const currentDate = new Date();
//   const startTime = currentDate.getTime();
//   let sum = 0;
//   for (i = 0; i < n; i++) {
//     sum += i;
//   }
//   const finalTime = currentDate.getTime();
//   const time = finalTime - startTime;
//   console.log(`${time / 1000} seconds`);
// }

// this is wrong because we are using the same date object to get the time and the time is not changing so we are getting the same time for all the calculations
// we have to initialize the date object again to get the correct time for the calculations
//initializa at start and then at the end of the calculations

//correct way -------->
// function calculateTime(n) {
// intialize at start 
//   const startTime = new Date().getTime();

//   let sum = 0;
//   for (i = 0; i < n; i++) {
//     sum += i;
//   }
//   const finalTime = new Date().getTime();
// intialize at the end
//   const time = finalTime - startTime;
//   console.log(`${time / 1000} seconds`);
// }


--------------------------------------------------------------------
/*
  Implement a class `Calculator` having below methods
    - initialise a result variable in the constructor and keep updating it after every arithmetic operation
    - add: takes a number and adds it to the result
    - subtract: takes a number and subtracts it from the result
    - multiply: takes a number and multiply it to the result
    - divide: takes a number and divide it to the result
    - clear: makes the `result` variable to 0
    - getResult: returns the value of `result` variable
    - calculate: takes a string expression which can take multi-arithmetic operations and give its result
      example input: `10 + 2 * ( 6 - (4 + 1) / 2) + 7`
      Points to Note: 
        1. the input can have multiple continuous spaces, you're supposed to avoid them and parse the expression correctly
        2. the input can have invalid non-numerical characters like `5 + abc`, you're supposed to throw error for such inputs

  Once you've implemented the logic, test your code by running
*/

class Calculator {
  constructor() {
    this.result = 0; // Initialize result to 0
  }

  // Adds a number to the result
  add(number) {
    this.result += number;
  }

  // Subtracts a number from the result
  subtract(number) {
    this.result -= number;
  }

  // Multiplies the result by a number
  multiply(number) {
    this.result *= number;
  }

  // Divides the result by a number
  divide(number) {
    if (number === 0) {
      throw new Error("Division by zero is not allowed");
    }
    this.result /= number;
  }

  // Resets the result to 0
  clear() {
    this.result = 0;
  }

  // Returns the current value of result
  getResult() {
    return this.result;
  }

  // Evaluates a string expression and updates the result
  calculate(expression) {
    // Remove unnecessary spaces
    const sanitizedExpression = expression.replace(/\s+/g, "");

    // Validate the expression
    if (!/^[\d+\-*/().]+$/.test(sanitizedExpression)) {
      throw new Error("Invalid expression: contains non-numerical characters");
    }

    try {
      // Use `eval` to evaluate the expression, but in a controlled manner
      const evaluatedResult = new Function(
        `return (${sanitizedExpression});`
      )();
      if (typeof evaluatedResult !== "number" || isNaN(evaluatedResult)) {
        throw new Error("Invalid expression");
      }
      this.result = evaluatedResult;
    } catch (error) {
      throw new Error("Error evaluating the expression");
    }
  }
}

module.exports = Calculator;

// Explanation ----
// 1. Class Properties and Methods:
// result: The internal state of the calculator.
// add, subtract, multiply, divide: Basic arithmetic operations that modify the result.
// clear: Resets result to 0.
// getResult: Returns the current value of result.
// calculate: Evaluates a string expression and updates the result.

// 2. calculate Method:
// Removes unnecessary spaces from the expression using replace.
// Validates that the input contains only valid characters (numbers, operators, parentheses).
// Uses new Function for safe evaluation of the expression.
// Updates the result with the evaluated value.

// 3. Error Handling:
// Throws errors for invalid characters in the input.
// Handles cases like division by zero or invalid expressions.

// Usage Example
const Calculator = require("./Calculator");

const calc = new Calculator();

// Basic operations
calc.add(10);
console.log(calc.getResult()); // 10

calc.subtract(2);
console.log(calc.getResult()); // 8

calc.multiply(5);
console.log(calc.getResult()); // 40

calc.divide(2);
console.log(calc.getResult()); // 20

calc.clear();
console.log(calc.getResult()); // 0

// Complex calculation
calc.calculate("10 + 2 * (6 - (4 + 1) / 2) + 7");
console.log(calc.getResult()); // 24

// Key Notes

// -- Security:
// eval is avoided in favor of new Function to minimize risks.
// Input is sanitized and validated before evaluation.

// -- Edge Cases:
// Handles invalid characters gracefully.
// Prevents division by zero.

-----------------------------------------------------------------
/*
  Implement a class `Todo` having below methods
    - add(todo): adds todo to list of todos
    - remove(indexOfTodo): remove todo from list of todos
    - update(index, updatedTodo): update todo at given index
    - getAll: returns all todos
    - get(indexOfTodo): returns todo at given index
    - clear: deletes all todos

  Once you've implemented the logic, test your code by running
*/

class Todo {
  constructor() {
    this.todos = [];
  }

  add(todo) {
    this.todos.push(todo);
  }
  remove(indexOfTodo) {
    this.todos.splice(indexOfTodo, 1);
  }
  update(index, updatedTodo) {
    if (index < 0 || index >= this.todos.length) {
      return;
    }
    this.todos[index] = updatedTodo;
  }
  getAll() {
    return this.todos;
  }
  get(indexOfTodo) {
    if (indexOfTodo < 0 || indexOfTodo >= this.todos.length) {
      return null;
    }
    return this.todos[indexOfTodo];
  }

  clear() {
    this.todos = [];
  }
}

module.exports = Todo;

```

### Async
```js
// ## Create a counter in JavaScript
// We have already covered this in the second lesson, but as an easy recap try to code a counter in Javascript
// It should go up as time goes by in intervals of 1 second

let counter = 0;
function increaseAndPrint() {
  counter = counter + 1; // counter++ ;
  console.log(counter);
}
setInterval(increaseAndPrint, 1000);


-----------------------------------------------------------------

// ## Counter without setInterval
// Without using setInterval, try to code a counter in Javascript

let counter = 0;
function increaseAndPrint() {
  counter = counter + 1; //counter++ ;
  console.log(counter);
  setTimeout(increaseAndPrint, 1000);
}
setTimeout(increaseAndPrint, 1000);

-----------------------------------------------------------------

// ## Reading the contents of a file
// Write code to read contents of a file and print it to the console.
// You can use the fs library to as a black box, the goal is to understand async tasks.
// Try to do an expensive operation below the file read and see how it affects the output.
// Make the expensive operation more and more expensive and see how it affects the output.

const fs = require("fs");
const filePath = "a.txt";

fs.readFile(filePath, "utf8", (err, data) => {
  if (err) {
    console.error("Error reading file:", err);
    return;
  }
  console.log("File content:", data);

  // Perform the expensive operation after file read completes
});

function expensiveOperation() {
  let sum = 0;
  for (let i = 0; i < 1e8; i++) {
    // Simulating a very expensive operation
    sum += i;
  }
  console.log("Expensive operation result:", sum);
}

expensiveOperation();
-----------------------------------------------------------------


// ## Write to a file
// Using the fs library again, try to write to the contents of a file.
// You can use the fs library to as a black box, the goal is to understand async tasks.

const fs = require("fs");
const data = "This is the content to write to the file.";

function expensiveOperation() {
  let sum = 0;
  for (let i = 0; i < 1e8; i++) {
    // Simulating a very expensive operation
    sum += i;
  }
  console.log("Expensive operation result:", sum);
}

fs.writeFile("a.txt", data, (err) => {
  if (err) {
    console.error("Error writing file:", err);
    return;
  }
  console.log(`Data written to a.txt`);
});

expensiveOperation();
-----------------------------------------------------------------


// Using `1-counter.md` or `2-counter.md` from the easy section, can you create a
// clock that shows you the current machine time?
// Can you make it so that it updates every second, and shows time in the following formats -

//  - HH:MM::SS (Eg. 13:45:23)
//  - HH:MM::SS AM/PM (Eg 01:45:23 PM)

function formatTime(date, use24Hour = true) {
  const hours = use24Hour ? date.getHours() : date.getHours() % 12 || 12;
  const minutes = date.getMinutes().toString().padStart(2, "0");
  const seconds = date.getSeconds().toString().padStart(2, "0");
  const ampm = use24Hour ? "" : date.getHours() >= 12 ? "PM" : "AM";

  return `${hours.toString().padStart(2, "0")}:${minutes}:${seconds}${
    ampm ? " " + ampm : ""
  }`;
}

function displayTime() {
  const now = new Date();
  const time24 = formatTime(now);
  const time12 = formatTime(now, false);

  console.clear();
  console.log(`24-hour format: ${time24}`);
  console.log(`12-hour format: ${time12}`);
}

function startClock() {
  displayTime();
  setInterval(displayTime, 1000);
}

startClock();
console.log("Press Ctrl+C to stop the clock.");
-----------------------------------------------------------------


// ## File cleaner
// Read a file, remove all the extra spaces and write it back to the same file.

// For example, if the file input was
// ```
// hello     world    my    name   is       raman
// ```

// After the program runs, the output should be
// ```
// hello world my name is raman
// ```

const fs = require("fs").promises;

async function cleanFile(filename) {
  try {
    // Read the file
    const content = await fs.readFile(filename, "utf8");

    // Remove extra spaces
    const cleanedContent = content.replace(/\s+/g, " ").trim();

    // Write back to the same file
    await fs.writeFile(filename, cleanedContent);

    console.log(`File '${filename}' has been cleaned.`);
  } catch (error) {
    console.error("Error:", error.message);
  }
}

// Usage
const filename = "a.txt";
cleanFile(filename);

-----------------------------------------------------------------

/*
    Write a function that returns a promise that resolves after n seconds have passed, where n is passed as an argument to the function.
*/

function wait(n) {
  return new Promise((resolve) => {
    setTimeout(resolve, n * 1000); // Convert seconds to milliseconds
  });
}

module.exports = wait;

// Explanation
// The wait function takes n as an argument, which represents the number of seconds to wait.
// A Promise is returned, which wraps the asynchronous operation // setTimeout:
// The setTimeout function is used to execute resolve after n * 1000 milliseconds (as setTimeout takes time in milliseconds).
// Once the timer completes, the resolve function is called to fulfill the promise.

// Usage Example ----------------------------------------------------------
const wait = require("./wait");
wait(2).then(() => {
  console.log("2 seconds have passed");
});
// This will log "2 seconds have passed" after waiting for 2 seconds.

-----------------------------------------------------------------


/*
 * Write a function that halts the JS thread (make it busy wait) for a given number of milliseconds.
 * During this time the thread should not be able to do anything else.
 * the function should return a promise just like before
 */

//synchoronous approach -- using a while loop
//not recommended as it will block the main thread and will not allow other tasks to be executed leading to degrade  performance

// function sleep(milliseconds) {
//   return new Promise((resolve) => {
//     const start = Date.now(); // Get the current time
//     while (Date.now() - start < milliseconds) {
//       // Busy-wait until the desired time has passed
//     }
//     resolve(); // Resolve the promise after busy-waiting
//   });
// }
// module.exports = sleep;

// Explaination
// - A while loop continuously checks the difference between the current time (Date.now()) and the start time until the desired milliseconds duration has elapsed.
// - The function wraps the busy-wait logic in a Promise that resolves once the loop finishes.
// -  This implementation blocks the JavaScript thread completely, meaning no other tasks (like rendering or event handling) can occur during the sleep duration.

// Usage Example --->
// const sleep = require('./sleep');
// console.log('Start');
// sleep(2000).then(() => {
//     console.log('2 seconds later');
// });

// Output  --->
// Start
// [Busy waiting...]
// 2 seconds later

// This method Completely blocks the event loop, preventing other asynchronous tasks leading bad performance. It's better to use asynchronous methods like setTimeout or async/await for non-blocking delays.

//
//----------------------------------------------------------------------------------------------------------------------------
//

// async approach using setTimeout
//  approach does not block the main thread and allows other tasks to be executed

function sleep(milliseconds) {
  return new Promise((resolve) => {
    setTimeout(resolve, milliseconds);
  });
}

module.exports = sleep;

// Explanation
// Using setTimeout, the function allows the JavaScript thread to remain free for other operations during the sleep period.
// Other asynchronous tasks, UI rendering, and event handling can continue while waiting.
// The Promise allows you to chain operations or use async/await for cleaner asynchronous code.

// Usage Example --->
const sleep = require("./sleep");
async function example() {
  console.log("Start");
  await sleep(2000); // Pause execution for 2 seconds
  console.log("2 seconds later");
}
example();

// Output --->
// Start
// [Waits for 2 seconds...]
// 2 seconds later

-----------------------------------------------------------------
Promise all

/*
 * Write 3 different functions that return promises that resolve after t1, t2, and t3 seconds respectively.
 * Write a function that uses the 3 functions to wait for all 3 promises to resolve using Promise.all,
 * Return a Promise.all which returns the time in milliseconds it takes to complete the entire operation.
 */

function wait1(t) {
  return new Promise((resolve) => {
    setTimeout(resolve, t * 1000);
  });
}

function wait2(t) {
  return new Promise((resolve) => {
    setTimeout(resolve, t * 1000);
  });
}

function wait3(t) {
  return new Promise((resolve) => {
    setTimeout(resolve, t * 1000);
  });
}

function calculateTime(t1, t2, t3) {
  const start = Date.now();
  return Promise.all([wait1(t1), wait2(t2), wait3(t3)]).then(() => {
    const end = Date.now();
    return end - start; // Return the total time taken in milliseconds
  });
}

module.exports = calculateTime;

//Explanation:
// 1. Functions wait1, wait2, and wait3:
// -- Each function returns a Promise that resolves after t seconds.
// -- Internally, they use setTimeout to delay the resolution.
// 2. Function calculateTime:
// -- Records the current time (start) using Date.now() before calling the Promise.all method.
// -- Promise.all waits for all the provided promises to resolve.
// -- After all promises resolve, the total time taken is calculated as end - start.
// 3. Output:
// -- The calculateTime function returns the total elapsed time in milliseconds.

// Usage Example --->
const calculateTime = require("./calculateTime");
calculateTime(1, 2, 3).then((time) => {
  console.log(`Total time taken: ${time} ms`);
});

// Output --->
// Total time taken: 3000 ms
// This reflects the maximum of t1, t2, and t3 because Promise.all resolves when all promises have completed.

-----------------------------------------------------------------
Promise chain

/*
 * Write 3 different functions that return promises that resolve after t1, t2, and t3 seconds respectively.
 * Write a function that sequentially calls all 3 of these functions in order.
 * Return a promise chain which returns the time in milliseconds it takes to complete the entire operation.
 * Compare it with the results from 3-promise-all.js
 */

function wait1(t) {
  return new Promise((resolve) => {
    setTimeout(resolve, t * 1000);
  });
}

function wait2(t) {
  return new Promise((resolve) => {
    setTimeout(resolve, t * 1000);
  });
}

function wait3(t) {
  return new Promise((resolve) => {
    setTimeout(resolve, t * 1000);
  });
}

function calculateTime(t1, t2, t3) {
  const start = Date.now();
  return wait1(t1)
    .then(() => wait2(t2))
    .then(() => wait3(t3))
    .then(() => {
      const end = Date.now();
      return end - start; // Return the total time taken in milliseconds
    });
}

module.exports = calculateTime;

// Explanation
// 1. Functions wait1, wait2, and wait3:
// -- Each function returns a Promise that resolves after t seconds, similar to the implementation in the previous example.
// 2. Sequential Execution in calculateTime:
// -- Starts by recording the time using Date.now().
// -- Calls wait1, waits for it to resolve, then calls wait2, and so on.
// -- Uses .then chaining to ensure the calls are sequential.
// 3. Time Measurement:
// -- The total time is calculated as the difference between the start and end times.
// -- The total time is returned as the result of the promise chain.

// Usage Example --->
const calculateTime = require("./calculateTime");
calculateTime(1, 2, 3).then((time) => {
  console.log(`Total time taken: ${time} ms`);
});

// Expected Output:
// Total time taken: 6000 ms
// This is because the functions are executed sequentially, and the total time is the sum of t1, t2, and t3.

// Comparison with Promise.all
// In the Promise.all version, all promises run concurrently, so the total time is the maximum of t1, t2, and t3.
// In the sequential version, each promise must complete before the next starts, so the total time is the sum of t1, t2, and t3. Which is so signifiacntly more than the Promise.all version.


-----------------------------------------------------------------


```