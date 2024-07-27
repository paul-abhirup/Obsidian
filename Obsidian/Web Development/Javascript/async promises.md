refference -
- https://www.freecodecamp.org/news/javascript-async-await-tutorial-learn-callbacks-promises-async-await-by-making-icecream/
- https://www.jsv9000.app/

async vs sync 
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

callback hell  
aka "nested callback"
when callbacks are nested one over the other 
issue -
-difficult to debug 
-not clean 
So, we use promises to deal with them 
classical structure of callback hell
```jsx

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

{new} keyword      
///creates a instance " prototype " of an object ///
These are the following features to use the new keyword:
- The new keyword creates a new empty object, with a type of object.
- The new keyword sets the internal prototype property of the constructing function.
- The new keyword binds this variable to the newly created object.
- The new keyword returns the new object.


Promises 
promises makes relationships between parent, child, grandchild ,.....

promise cycle

```jsx
// // Promise, promise chanining, .then, .catch, .finally
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


Async 
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