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