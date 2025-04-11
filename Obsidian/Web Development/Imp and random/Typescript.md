# Interfaces
```ts

interface User {
  firstName: string;
  lastName: string;
  email: string;
  phone?: string;// optional
  age: number;
}

// user1 object adheres to the User interface
const user1: User = {
  firstName: "harkirat",
  lastName: "singh",
  email: "email@gmail.com",
  age: 21,
};

// Problem: Create a function isLegal that returns true or false if a user is above 18. It takes a user as an input.

function isLegal(user: User): boolean {
  return user.age > 18;
}

```

```ts
interface Todo {
  title: string;
  text: string;
}

const todo1: Todo = {
  title: "organize desk",
  text: "clear clutter",
};

function showTodo(todo: Todo) {
  console.log(todo.title + " : " + todo.text);
}

```

```ts
//Problem: Create a React component that takes todos as an input and renders them.

// defines the interface of Todo
interface TodoType {
  title: string;
  description: string;
  done: boolean;
}

//specify the input prop for the todo component
interface TodoInput {
  todo: TodoType;
}

// Create a React component 'Todo' that takes a 'todo' prop and renders its properties ( title. description)
export default function Todo({ todo }: TodoInput) {
  return (
    <div>
      <h1>{todo.title}</h1>
      <h2>{todo.description}</h2>
      <h2>{todo.done ? "Done" : "Not Done"}</h2>
    </div>
  );
}

```
todo is doesnt exit on the type TodoType
So, its imp to define that the 'todo' prop exist and defined on the interface TodoInput

although this is true, if we use  object-destructuring
`{title, description, done}: TodoType`
but this is wrong accn to react logic, as they are not props

alternate approach 
```ts
export default function Todo({todo}: TodoInput){
 const {title, description, done}: TodoType = todo
 }
```

### Implementing Interfaces
By implementing interfaces as class, we provide a way to define a blueprint for the structure and behaviour of the class

```ts

interface Person {
  name: string;
  age: number;
  greet(phrase: string): void;
}

class Employee implements Person {
  name: string;
  age: number;

  constructor(n: string, a: number) {
    this.name = n;
    this.age = a;
  }

  greet(phrase: string) {
    console.log(`${phrase} ${this.name}`);
  }
}

// its good for creating different types of person ensuring they adhers to the same interface.
// maintain a consistent structure accross different classes


```

the JS code for the TS code
```js
class Employee {
    constructor(n, a) {
        this.name = n;
        this.age = a;
    }
    greet(phrase) {
        console.log(`${phrase} ${this.name}`);
    }
}

```

# Types 
In ts, types are just like interfaces -- a way to define the structure of an object.

```ts
type User = {
    firstName: string;
    lastName: string;
    age: number;
};
```

##### Features --
- Unions
	 Allows you to define a type that can have 2 or more types.
	 Unions provide felxibility in handling different types within a single type defination.
	 
	 ```ts
		type StringOrNumber = string | number;

		function printId(id: StringOrNumber) {
		  console.log(`ID: ${id}`);
		}
		
		printId(101);     // ID: 101
		printId("202");   // ID: 202
```

- Intersection
	Allows you to create a type that has every property of multiple types or interfaces.
	Provide a way to create a new type that inherits properties from multiple existing types or interfaces.
	
	```ts
	
	type Employee = {
	  name: string;
	  startDate: Date;
	};
	
	type Manager = {
	  name: string;
	  department: string;
	};
	
	type TeamLead = Employee & Manager;
	
	const teamLead: TeamLead = {
	  name: "harkirat",
	  startDate: new Date(),
	  department: "Software Developer"
};
	
```

### Types VS Interfaces

|        Point of Difference         | Types                                                                                                                                    | Interfaces                                                                                                                        |
| :--------------------------------: | :--------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
|         Declaration Syntax         | flexible syntax, can represent primitive types, unions, intersections, and more                                                          | Typically used for defining the structure of an object                                                                            |
|       Extension and Merging        | - supports extended types<br><br>- cant be merged if you define another type with the same name, it will just overrides the previous one | - Supports extending interfaces using the extends keyword.<br><br>- merges the same name interfaces, combining their declarations |
| Decalaration <br>Vs Implementation | - suitable for describing the shape of the data <br><br>- represent any type, including primitives, unions, intersections, etc.          | - used to define contracts for classes<br><br>- mainly used to define the shape of the object                                     |
|          Type Overriding           | - cannot be overridden, if so replaces the old one with the new one                                                                      | - merges if have the same name                                                                                                    |
|   Object literal <br>strictness    | - lineant                                                                                                                                | - strict                                                                                                                          |

Type Example - 
```ts
type StringOrNumber = string | number;

function printId(id: StringOrNumber) {
  console.log(`ID: ${id}`);
}

printId(101);       // ID: 101
printId("202");     // ID: 202
```

// if anything can be done by interefaces try to do it by interfaces
// if not then only try to use types
```ts

interface Manager {
    name: string;
    age: number;
    region: string;
}
// interfaces can be implemented as classes

type Techlead = {
    name: string;
    age: number;
    company: string;
}
// types lets u do unions and intersections

function x(m: Manager){
    // code ....
}

type Boss = Manager & Techlead;
```


# Generics
```ts
function getFirstElement<T>(arr: T[]) {
    return arr[0];
}

const el = getFirstElement(["harkiratSingh", "ramanSingh"]);
const el2 = getFirstElement([true,false]);
const el3 = getFirstElement([1,2,3,4,5])

console.log(el.toLowerCase())
// this is not givnig an error as the output is of type number


const el4 = getFirstElement(["harkiratSingh","ramanSingh",1, 2]);
// here the tsc assumes that the template is a (string | number) 

// so to prevent this issue we define the variable type, so the person cant give you anything other than the string 
const el5 = getFirstElement<string>(["harkiratSingh","ramanSingh",1, 2]);


// Also we define user-defined data types 
interface User {
    name: string
}

const el6 = getFirstElement<User>([{name: "Paul"}]);
el6.name;
```

----
---
---
# Hitesh class Ts

ts is just about type-safety

ts is not a language, it is a build-tool
ts trives in static-checking. It prevents the code from runtime error by gving the errors before hand.

-- you ca use the ts docs for the custom tsconfig.json generation 

// For this code we will be using ts doc -- Everyday types 

**basic js types**  ---- 
- number   // as js doesnt have anything special for `int` or `float`
- string
- boolean
- *null
- *undefined
- void
- never

Less common primitives like --
bigint
symbol

more advancces types in ts --- 
objects 
tuples
arrays
typles

**Type annotation**
when you give types to a declared variable.
`const variableTitle: string = "Paul" `
### Any
also using [ any ] to write more javascriptish code 
In ts using any just turns off the type checking for the variable

but in ts we need to prevent [ any ] as much as possible

You usually want to avoid this, though, because `any` isn’t type-checked. Use the compiler flag [`noImplicitAny`](https://www.typescriptlang.org/tsconfig#noImplicitAny) to flag any implicit `any` as an error.

## function.ts
```ts

// Parameter Type Annotation
// Return Type Annotation
function addTwo(num: number): number{
     return num + 2 ;
    //return "hello";
}

let myValue = addTwo(5);

function getUpper(val: string){
    return val.toUpperCase();
}

getUpper("hitesh");

function signUpUser(name: string, email: string, isPaid: boolean){}

let loginUser = (name: string, email: string, isPaid: boolean = false) => {}


signUpUser("hitesh", "hitesh@lco.dev", false);
loginUser("h", "h@h.com");

// function getValue(myVal: number): boolean{
//     if (myVal > 5) {
//         return true
//     }
//     return "200 OK"
// }

// here the function is returning more than 1 type 

const getHello = (s: string):string => {
    return ""
}

const heros = ["thor", "spiderman", "ironman"]
// const heros = [1, 2, 3]

// in ts it auto detects the type of the (hero) due to ts context-switching 
heros.map((hero): string => {
    return `hero is ${hero}`
})

// console the error 
function consoleError(errmsg: string): void{
    console.log(errmsg);
}

// handles the error
function handleError(errmsg: string): never{
    throw new Error(errmsg);    
}
// using "never" is used to never read the return type of the function


// function which return promises
async function getFavoriteNumber(): Promise<number> {
  return 26;
}

```


## Objects.ts
```ts
const User1 = {
    name: "hitesh",
    email: "hitesh@lco.dev",
    isAvtive: true
}

function createUser({name: string; isPaid: boolean}){};
//You can use `,` or `;` to separate the properties, and the last separator is optional either way.

let newUser = {name: "hitesh", isPaid: false, email: "h@h.com"}

createUser(newUser);

function createCourse():{name: string, price: number}{
    return {name: "reactjs", price: 399}
}
```

```ts
type User = {
    name: string;
    email: string;
    isActive: boolean
}


function createUser(user: User): User{
    return {name: "", email: "", isActive: true}
}

createUser({name: "Paul", email: "paul1249@gmail.com", isActive: true})


```

Readonly and optional
```ts
type User = {
    readonly _id: string
    name: string
    email: string
    isActive: boolean
    credcardDetails?: number  //optional
}

let myUser: User = {
    _id: "1245",
    name: "h",
    email: "h@h.com",
    isActive: false
}

type cardNumber = {
    cardnumber: string
}

type cardDate = {
    cardDate: string
}

type cardDetails = cardNumber & cardDate & {
    cvv: number
}


myUser.email = "h@gmail.com"
// myUser._id = "asa" //error as it is readonly

```

## Array.ts
```ts
const superHeros: string[] = []
// const heroPower: number[] = []
const heroPower: Array<number> = []

superHeros.push("spiderman");
heroPower.push(2);

type User = {
    name: string
    isActive: boolean
}

const allUsers: User[] = []

const MLModels: number[][] = [
    [255, 255, 255],
    []
]


allUsers.push({name: "king", isActive: true});
```

## Union.ts
```ts
let score: number | string = 33
score = 44
score = "55"


type User = {
    name: string;
    id: number
}

type Admin = {
    username: string;
    id: number
}

let hitesh: User | Admin = {name: "hitesh", id: 334}

hitesh = {username: "hc", id: 334}

// function getDbId(id: number | string){
//     //making some API calls
//     console.log(`DB id is: ${id}`);
    
// }
getDbId(3)
getDbId("3")

function getDbId(id: number | string){
    if (typeof id === "string") {
        id.toLowerCase()
    }
  
}

//array 

const data: number[] = [1, 2, 3]
const data2: string[] = ["1", "2", "3"]
const data3: (string | number | boolean)[] = ["1", "2", 3, true]

let seatAllotment: "aisle" | "middle" | "window"

seatAllotment = "aisle"
// seatAllotment = "crew"
```

## Tuples
```ts

// const user: (string | number)[] = [1, "hc"]

// creating tuples 
// this creates a strong pattern like =>  string then number then boolean
let tUser: [string, number, boolean]

tUser = ["hc", 131, true] // correct 

// tUSer = [23, false, "pal"]  // wrong as it doesnt follow the pattern

let rgb: [number, number, number] = [255, 123, 112]

type User = [number, string];

const newUser: User = [112, "example@google.com"]

newUser[1] = "hc.com" ;   // overriding the email
newUser.push(true);

```


## interface.ts
```ts
interface User {
    readonly dbId: number
    email: string,
    userId: number,
    googleId?: string,
    // startTrail: () => string   
    startTrail(): string,   // method 
    getCoupon(couponname: string, value: number): number
}

interface User {
    githubToken: string
}

// you can use interface to inherit properties 
interface Admin extends User {
    role: "admin" | "ta" | "learner"
}

const hitesh: Admin = { dbId: 22, email: "h@h.com", userId: 2211,
role: "admin",
githubToken: "github",
startTrail: () => {
    return "trail started";
},
getCoupon: (name: "hitesh10", off: 10) => {
    return 10;
}
}
hitesh.email = "h@hc.com"; //changing the email
// hitesh.dbId = 33   // wrong because its a readonly property 

```

setting up ts in real-world projects
tsconfig.json
```bash
    "target": "es2016",                                  /* Set the JavaScript language version for emitted JavaScript and include compatible library declarations. */

    "module": "commonjs",             /* Specify what module code is generated. */

    "outDir": "./dist",                                   /* Specify an output folder for all emitted files. */

    "esModuleInterop": true,                             /* Emit additional JavaScript to ease support for importing CommonJS modules. This enables 'allowSyntheticDefaultImports' for type compatibility. */

    "forceConsistentCasingInFileNames": true,            /* Ensure that casing is correct in imports. */


    "strict": true,                                      /* Enable all strict type-checking options. */


    "skipLibCheck": true                                 /* Skip type checking all .d.ts files. */

```

## Class in TS
revise class in js -- constructor, etc
?? why the city property is not passed into the constructor

```ts
class User {
     email: string
     name: string
    //  city: string = ""    
    readonly city: string = "Delhi"
    constructor(email: string, name: string){
        this.email = email;
        this.name = name;

    }
}

const user1 = new User("abhir@paul.com", "paul");
// user1.city = "Jaipur";

```


```ts
class User {
    public email: string
    private name: string
    readonly city: string = "Jaipur"
    constructor(email: string, name: string){
        this.email = email;
        this.name = name
    }
}

const user1 = new User("abhir@paul.com", "paul");
// user1.name   
// this is wrong becuase it is private and only accessible inside the class

// better approach
class Userbsdk {
    readonly city: string = "Jaipur"
    constructor(public email: string, private name: string){
        this.email = email;
        this.name = name
    }
}
```


```ts
class User {

    // private _courseCount = 1;  //only accesible within the class

    protected _courseCount = 1;
    // we use protected instead of private to make sure the inherited class also herits this prop
        
    readonly city: string = "Jaipur"
    constructor(
        public email: string, 
        public name: string,
        // private userId: string
        ){
    }

    // private method 
    private deleteToken(){
        console.log("Token deleted");        
    }

    get getAppleEmail(): string{
        return `apple${this.email}`
    }

    get courseCount(): number {
        return this._courseCount
    }

    //'set' accessor cant have a return type annotation
    // set courseCount(courseNum): void {}   // worng 
    // ts want nothing to as return as setter is accesing an property to set it

    set courseCount(courseNum) {
        if (courseNum <= 1) {
            throw new Error("Course count should be more than 1")
        }
        this._courseCount = courseNum
    }
}

// inheritance 
// while creating this it will acquire all the properties of the User except the private properties as it is not accesible outside the class
// so will be using protected to inherit the props 

class SubUser extends User {
    isFamily: boolean = true
    changeCourseCount(){
        this._courseCount = 4
    }
}


const hitesh = new User("h@h.com","hitesh")

// hitesh.deleteToken()
// not allowed as it is a private property within the class 
```

## Interface Example
```ts
interface TakePhoto {
    cameraMode: string
    filter: string
    burst: number
}

interface Story {
    createStory(): void
}

// implements is used only for the interface 
// interface is being implemented by this class
class Instagram implements TakePhoto {
    constructor(
        public cameraMode: string,
        public filter: string,
        public burst: number
    ){}
}

class Youtube implements TakePhoto, Story{
    constructor(
        public cameraMode: string,
        public filter: string,
        public burst: number,
        public short: string
    ){}

    createStory(): void {
        console.log("Story was created");
        
    }
}
```

## Abstract Class
```ts
// now new object can be created from an abstract class
abstract class TakePhoto {
    constructor(
        public cameraMode: string,
        public filter: string
    ){}
    
    //creating methods in abstract class

    // abstract method
    abstract getSepia(): void

    //abstract method ---> means that the method doesnt provide any defination but needs to get implemented otherwise will give an error
    
    //
    getReelTime(): number{
        //some complex calculation
        return 8
    }
}

// using class in another class 
class Instagram extends TakePhoto{
    constructor(
        public cameraMode: string,
        public filter: string,
        public burst: number
        ){
            super(cameraMode, filter)
        }

        getSepia(): void {
            console.log("Sepia");            
        }
}

const hc = new Instagram("test", "Test", 3);
// 3 is being passed into the class for getReelTime func.

hc.getReelTime()
```

abstract classes dont define objects of their own 
You need to define them 


## Generics 
```ts
const score: Array<number> = []
const names:Array<string> = []

//why need Generics
function identityOne(val: boolean | number): boolean | number{
    return val
}

// using any : is not good 
function identityTwo(val: any):any{
    return val
}

// using generics
function identityThree<Type>(val: Type): Type {
    return val
}

// identityThree(true);
identityThree(3);    // the value is providing is 3 and the return is also of type 3 
/*  function identityThree<3>(val: 3): 3   */


// syntactical-sugar
function identityFour<T>(val: T): T {
    return val
}

interface Bootle{
    brand: string,
    type: number
}

identityFour<Bootle>({});  
//mean this --->  function identityFour<Bootle>(val: Bootle): Bootle

// you need to set custom types like <Bootles> when you are using user defined data-types

```

generics in array
```ts

function getSearchProducts<T>(products: T[]): T {
    // do some database operations
    const myIndex = 3
    return products[myIndex]
}

// <T,> this is heavily used in React JSX, instead of <T>
// because this is how in JSX  we symbolize Generics 
const getMoreSearchProducts = <T,>(products: T[]): T => {
    //do some database operations
    const myIndex = 4
    return products[myIndex]
}
```

## generics class
```ts
interface Database {
    connection: string,
    username: string,
    password: string
}

function anotherFunction<T, U extends Database>(valOne:T, valTwo:U):object {
    return{
        valOne,
        valTwo
    }
}

// anotherFunction(3, {})



// create a class where there could be a course or a quiz; and there will be methods for both of them
interface Quiz{
    name: string,
    type: string
}

interface Course{
    name: string,
    author: string,
    subject: string
}

//create a generics class
class Sellable<T>{
    public cart: T[] = []
    //intialize an empty array --> cart of the type T 

    //method
    addToCart(product: T){
        this.cart.push(product)
    }
}
```

```ts
//type narrowing

function detectType(val: number | string ){
    if (typeof val === "string") {
        return val.toLowerCase();
    }
    return val + 3
}

function provideId(id: string | null){
    if(!id){
        console.log("Please provide ID");
        return
    }
    id.toLowerCase();
}


// in ts array also results into a type of "object"
// typeof ["a", "b", "c"]  ===> object
// typeof "paul" ==> string

function printAll(strs: string | string[] | null) {
    
    if (strs) {
      if (typeof strs === "object") {
        for (const s of strs) {
          console.log(s);
        }
      } else if (typeof strs === "string") {
        console.log(strs);
      }
    }
  }

```

```ts
// in operator narrowing

interface User {
    name: string,
    email: string
}

interface Admin{
    name: string,
    email: string,
    isAdmin: boolean
}

function isAdminAccount(account: User | Admin){
    if ("isAdmin" in account) {
        // if this prop "isAdmin" exist in this account
        return account.isAdmin
    }
}
```