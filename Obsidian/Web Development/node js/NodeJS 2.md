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