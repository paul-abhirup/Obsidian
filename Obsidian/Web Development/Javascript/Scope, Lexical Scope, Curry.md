Scope --> area where an item(func, variable) can be accesible
- Global Scope --> available globally, can be used locally
- Local Scope --> available locally only, cant be used globally

#### Scope Chain
```js
const f1 = "mclaren";
function f2(){
  function f3(){
    function f4(){
      return f1;
    }
    return f4();
  }
  return f3();
}

//calling f2();
f2();
```
lexical scope -->means "origin" 
#### Working of Lexical Chain
- How Scope Chain works ?
- finding lexical scope("origin") on f1 

In JS 
1) Js will check if f1 is defined locally within f4( ), if not it will move up the chain
2) check if f1 is in f3( ), if not move up the chain 
3) similarly check if f1 is in f2()
4) last check for gobal scope
5) in case, not find, JS returns "reference Error"

#### Lexical Scope in JS (alias, static scope)

lexical -> meaning creating words, expressions or variables
In dicationary -->alias "lexicon"

The place where an item is defined (item's defination space)/Origin
"defination space "  not " in"
Lexical environment --> Surrounding Space 

### Curry in Js

```js
// normal func
function add(a,b,c){
  return a+b+c;
}

//calling function
add(1,2,3);

//Curry
function add(a){
  return function(b){
    return function(c){
      return a+b+c;
    }
  }
}
add(2)(3)(5); //10
add(2)(3) //Error
//3 parameters are mandatory

//Using ES6 
const add = (a) => (b) => (c) => a+b+c;

```

