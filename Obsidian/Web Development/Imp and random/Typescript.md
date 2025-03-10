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

basic js types  ---- 
number
string
boolean
null
undefined
void

more advancces types in ts --- 
objects 
tuples
arrays
typles

also using [ any ] to write more javascriptish code 
In ts using any just turns off the type checking for the variable

but in ts we need to prevent [ any ] as much as possible

function.ts
```ts

```

