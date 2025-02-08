tsc compiler 


```ts
//ex --- 1
// const a: number = 1;
// const a = "harkirat";
// console.log(a);



// BASIC TYPES in TS ----------------------------------------------

// 1. Number
const a: number = 1;

// 2. String
const b: string = "harpreet";

// 3. Boolean
const c: boolean = true;

// 4. Undefined
const d: undefined = undefined;

// 5. Null
const e: null = null;

```

## Code Implementation and practice

### Hello world Greeting

- learn how to give types to function and arguments
```ts
// Write a TypeScript function named greet that takes a user's first name as an argument and logs a greeting message to the console.

function namePrint( name: string): void{
 console.log("hello ", name );
}

namePrint("Paul"); //trigger function
```

void -> as the function return nothing hence is of type void
name -> is of type string

### Sum Function

- assign a return type to a function
```ts
// Write a TypeScript function named sum that takes two numbers as arguments and returns their sum. Additionally, invoke the function with an example.

function sum(a: number, b: number): number {
  return a + b;
}

// this ensures that the function returns the expected data type

// but if it was like 
// function sumer(a: number, b: number): string {
//   return a + b;
// };
// give error because the return type is not the same as the function return type
```

### Age verification Function

- learning type-inference 
```ts
// Write a TypeScript function named isLegal that takes an age as a parameter and returns true if the user is 18 or older, and false otherwise. Also, invoke the function with an example.

function isLegal(age: number): boolean {
    if (age > 18) {
        return true;
    } else {
        return false;
    }
}

isLegal(12);
isLegal(19);
isLegal(22);

```

this describes that the tsc compiler can can automatically infer the tyoe of the variables based on the values assignes to them.

### Delayed Function Execution

- learn to work with function as parameter to a function
```ts
// Write a TypeScript function named delayedCall that takes another function (fn) as input and executes it after a delay of 1 second. Also, invoke the delayedCall function with an example.

function delayedCall(fn: () => void): void {
  // code
  setTimeout(fn, 1000);
}

// example
delayedCall(function () {
  console.log("Hello World!");
});

(fn: () => void)


```

this means that the function fn takes no arguments and returns void .

initializa ts by `npx tsc --init`
## tsconfig.json

1. target
		this specifies the ecma version for the ts
		so the code adhers the ecma version
		like "es5" or "es2020"
		
2. rootDir
		this specifies the compiler to look for the .ts files in this folder

3. outDir
		this specifies the comipler to generate the files in this folder 

4. notImpilcitAny
		tells whether tsc should give any error when it encounters a variable with an implicit 'any' type 
		false ---  false means that no error will be issued. for a variable with an implicit any type
		true ---  error will be published for such variables

5. removeComments

```ts
/// tsconfig


{
  "compilerOptions": {
    "target": "es2020", // scpecify the ecma version
    "module": "commonjs" /* Specify what module code is generated. */,
    "rootDir": "./src" /* Specify the root folder within your source files. */,
    "outDir": "./dist" /* Specify an output folder for all emitted files. */,
    "noImplicitAny": true, //determines whether TypeScript should issue an error when it encounters a variable with an implicit any type..
    "removeComments": true //determines whether comments should be removed from the generated JavaScript files.
  }
}


```


# Interfaces

- it is a way to define a contract tfor shape of the object 
- allows you to specify the expected properties, their types and also whether they are optional or needed

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

## Types 
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

Interface Example - 
```ts
interface Employee {
  name: string;
  startDate: Date;
}

interface Manager {
  name: string;
  department: string;
}

type TeamLead = Employee & Manager;

const teamLead: TeamLead = {
  name: "Harkirat",
  startDate: new Date(),
  department: "Software Developer",
};
```

## When to Use Which

- **Use Types:**
    - For advanced scenarios requiring union types, intersections, or mapped types and flexibility.
    - When dealing with primitive types, tuples, or non-object-related types.
    - Creating utility types using advanced features like conditional types.
- **Use Interfaces:**
    - Objects shape, contracts, class implementations.
    - Extending or implementing other interfaces.
    - When consistency in object shape is a priority.