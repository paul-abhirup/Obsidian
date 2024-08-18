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