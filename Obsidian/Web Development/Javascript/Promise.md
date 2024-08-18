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