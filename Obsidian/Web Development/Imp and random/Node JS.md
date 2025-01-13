#js #express

```jsx
//Instead  // const fs = require ('fs')  

//creating a http server using express
//express dont come by default in a node 
const express = require("express");

//creating the clinic
const app = express();

//request methods 
// GET - going for a check up
// POST - going for a new kidney insertion
// PUT -  going for kidney to get replaced
// DELETE - going to get kidney removed

//STATUS CODES
//200 - allowed
//404 - doctor not in hospital
//500 - mid surgey loadshedding
//411 - wrong person came
//403 -  not allowed in the hospital

/**   Assignment
 * create a in memory hospital [in-memory server : server that is not using a database]
 * You need to create 4 routes (4 things that the hospital can do)
1. GET - User can check how many kidneys they have and their health
2. POST - User can add a new kidney
3. PUT - User can replace a kidney, make it healthy
4. DELETE - User can remove a kidney
 */



const users = [{
    name: "John",
    kidneys: [{
        healthy: false
    }]
}];

// parses incoming req
// populates req.body
app.use(bodyParser.json());
//anytime there is json in the body of req this is used to deal with it 

//JSON parsing middleware
app.use(express.json());
//parses incoming requests with json payload
//for json body in the server


// you should use any one of this middleware not neccesary to use both of them , as they serve the same purpose - parses incoming req and populates req.body


// query parameters are true for GET request -- to send data by the user
app.get("/", function (req, res) {
    const johnKidneys = users[0].kidneys;
    const numberOfKidneys = johnKidneys.length;
    let numberOfHealthyKidneys = 0;
    for (let i = 0; i < johnKidneys.length; i++) {
        if (johnKidneys[i].healthy) {
            numberOfHealthyKidneys = numberOfHealthyKidneys + 1;
        }
    }
    const numberOfUnhealthyKidneys = numberOfKidneys - numberOfHealthyKidneys;
    res.json({
        numberOfKidneys,
        numberOfHealthyKidneys,
        numberOfUnhealthyKidneys
    })
})


//for post request data are being send in the body
app.post("/",function (req, res){
   console.log(req.body);   
   //this will be (undefined) without app.use(express.json()); as it parses the request body
   
    const isHealthy = req.body.isHealthy;
    
    //this line extracts the value of `isHealthy` property from the request body(`req.body`)
    //in express when u recieve data in PUT or POST request, it`s often sent in the request body.
    // this is essentially creating a variable `isHealthy` and assign it the value of `req.body.isHealthy`


    users[0].kidneys.push({
        healthy: isHealthy
    });
    
    //access the kidney array inside the user array and pushes an object in it
    //the object has a `healthy` property and its value is  assigned to the prev extracted `isHealthy` variable


    res.json({
        msg: "Done!"
    });
    
})

//on multiple post requests the get request gets updated
//ex- 
//{"numberOfKidneys":13,"numberOfHealthyKidneys":12,"numberOfUnhealthyKidneys":1}
//here its imp u use `app.use(express.json())`
//without it `isHealthy` is will be classified as `undefined`

//this is how the user request looks like 
//  {
//    "isHealthy": true
//   }

// 411
// update every kidney to be healthy
app.put("/", function (req, res) {
    for (let i = 0; i < users[0].kidneys.length; i++) {
        users[0].kidneys[i].healthy = true;
    }
    res.json({
    msg: "Done!"
    }); // if dont res back the request will hung
});
// any time u restart the process the user array gets reset 
// so we need datatbases to store user data ,because an in memory can easily lose data if the backend gets down



// removing all the unhealthy kidneys
app.delete("/", function (req, res) {
// atleast 1 unhealthy kidney is there do this, else return 411

function isThereAtleastOneUnhealthyKidney() {
    let atleastOneUnhealthyKidney = false;
    for (let i = 0; i < users[0].kidneys.length; i++) {
        if (!users[0].kidneys[i].healthy) {
            atleastOneUnhealthyKidney = true;
        }
    }
    return atleastOneUnhealthyKidney
}


    if (isThereAtleastOneUnhealthyKidney()) {
        const newKidneys = [];
        for (let i = 0; i < users[0].kidneys.length;i++) {
            if (users[0].kidneys[i].healthy) {
                newKidneys.push({
                    healthy: true
                })
            }
        }
        users[0].kidneys = newKidneys;
        res.json({ msg: "done" })
    } else {
        res.status(411).json({
            msg: "You have no bad kidneys"
        });
    }
})


//listening a specific port
//doctor siting in a room
app.listen(3000);

```

root -- starting point of all directory 
node index.js -- uses node to run the file 
- nodejs is made up of multiple modules -- fs, os, childprocess ,etc
   fs module , childprocess module , os module 
- js helps interacting the app with this modules 

filesystem(fs) module helps to interact with the files 

REPL - Read Evaluation Print Loop
node itself works in REPL

node contains a set of native node modules .
to export further more modules we need to export it in the app .
```jsx
//require the module
const fs - require("fs");
```

**NPM**
node module manager 
- libraries of JS files 
- they are dependencies used on several other 
- package manager for node 
- made of 
	- local packages 
	- global packages


```
npm i -g nodemon

-g ----- denotes global 
i -------- install 
```

#### package versioning
npm packages falls under semantic versioning 
ex   "11.11.11"
major patch > minor patch > patch 
major - huge upgrade 
minor - feature 
patch - bug solve 

if major patch changes, rest is 0
"2.0.0"
if minor patch changes, patch is 0
"2.9.0"
" ^5.0.1 "  ---- ( ^ ) this prevents from major update, so u manually update the packages 
```
npm i chalk@latest
```
So to allow dependencies to update latest packages we use ( ~ )
" ~1.3.8"

"npm init "
this create package.json --- which has all the dependencies required
package.json
- app info 
- dependencies(name and version),dev-dependencies
- creates npm scripts

```jsx
//change the name of the author
npm config set init-author-name "Brad"

//change license 
npm set init-license"MIT"

npm init -y

//get author name 
npm get init-author-name

//delete author name 
npm config delete init-author-name

npm i --production 
//install produiction dependency
```