refference -
- https://www.freecodecamp.org/news/javascript-async-await-tutorial-learn-callbacks-promises-async-await-by-making-icecream/
- https://www.jsv9000.app/

Async 
It builds on top of Promises and allows you to avoid chaining `.then()` and `.catch()` methods while still working with asynchronous operations.
```jsx

let stocks = {
    Fruits : ["strawberry", "grapes", "banana", "apple"],
    liquid : ["water", "ice"],
    holder : ["cone", "cup", "stick"],
    toppings : ["chocolate", "peanuts"],
 };

let is_shop_open = true;

//promise syntax
// let order = () => {
//     return new promise ((resolve,reject) => {
//         if(true){
//             resolve()
//         }else{
//             reject()
//         }
//     })
// }

// order()
// .then()
// .then()
// .then()
// .catch()
// .finally()


//async
async function order (){

    try{
        await abc;
    // abc is a fake fn as it doesnt exist 
    
    }
        
    catch(error){
        console.log("abc doesnt exist", error)
    }
        
    finally{
        console.log("runs any way");
    }
}

trigger fn
order();

order()
.then(() => {
console.log("hello")
})
.then()
.catch()
.finally()

//u can also use the try catch system outside the async
    // also simultanoeusly i.e u can use try catch inside the fn as well as within the trigger fn
    //although these then and catch will be executed after the inside code is being executed 
```

Await keyboard
```jsx

let stocks = {
    Fruits : ["strawberry", "grapes", "banana", "apple"],
    liquid : ["water", "ice"],
    holder : ["cone", "cup", "stick"],
    toppings : ["chocolate", "peanuts"],
 };

let is_shop_open = true;

let toppings_choice = () => {
    return new Promise( (resolve, reject) => {
        setTimeout(() => {
         resolve ( console.log("which toppings u like ?"));
        },3000);
    })
}


async function kitchen (){

    //chef making ice cream
    console.log("A");
    console.log("B");
    console.log("C");

    //chef realized to ask the customer for toppings
    //chef going out to ask customer about topping 
    await toppings_choice();

    //chef collects data from customer 
    //chef came back and continues with the ice cream process
    console.log("D");
    console.log("E");
    //chef finishes the ice cream

}
//trigger fn
kitchen();

//other chore works 
console.log("doing the dishes");
console.log("cleaning the table");
console.log("taking other orders");

```


```jsx

let stocks = {
    Fruits : ["strawberry", "grapes", "banana", "apple"],
    liquid : ["water", "ice"],
    holder : ["cone", "cup", "stick"],
    toppings : ["chocolate", "peanuts"],
 };

let is_shop_open = true;

function time(ms) {
   return new Promise( (resolve, reject) => {
      if(is_shop_open){
         setTimeout(resolve,ms);
      }
      else{
         reject(console.log("Shop is closed"))
      }
    });
}

async function kitchen(){
    try{
    await time(2000)
    console.log(`${stocks.Fruits[0]} was selected`)

    await time(0000)
    console.log("production has started")

    await time(2000)
    console.log("fruit has been chopped")

    await time(1000)
    console.log(`${stocks.liquid[0]} and ${stocks.liquid[1]} added`)

    await time(1000)
    console.log("start the machine")

    await time(2000)
    console.log(`ice cream placed on ${stocks.holder[1]}`)

    await time(3000)
    console.log(`${stocks.toppings[0]} as toppings`)

    await time(2000)
    console.log("Ice Cream served ")
    }

    catch(error){
     console.log("customer left")
    }
    finally{
        console.log("day ended store is closed ");
    }
}
// Trigger
kitchen();



```