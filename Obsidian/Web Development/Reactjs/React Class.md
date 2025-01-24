#react 
## React-Returns

create a react app that has a header component 
- that take title as a prop and renders it inside a div
- App renders more than 1 Header 
``` jsx
import React, { useState } from 'react'

function App() {

  return (

    //instead of returning multiple divs we can use react fragment
    //  <Header title="harkirat2" />  
    //   <Header title="harkirat3" />  
    //   <Header title="harkirat4" />  

    // like this 
      <>     
      <Header title="harkirat1" />  
      <Header title="harkirat2" />  
      <Header title="harkirat3" />  
      <Header title="harkirat4" />  
      </>
      
      //here the parent <> </>, ie React Fragment
      // <React.Fragment> </React.Fragment>
	//is returning multiple children component //this helps in returning multiple children

//// or 
	 <div>     
      <Header title="harkirat1" />  
      <Header title="harkirat2" />  
      <Header title="harkirat3" />  
      <Header title="harkirat4" />  
      </div>
		//ie //child component should have atleast 1 parent component
    
  )
}

function Header({title}){
  return <div>
  {title}
  </div>
}

export default App

```

## Re-rendering in React
  - every time a parent re-renders all the children re-render as well. 
  - so its important to render only the important elements and not all of them
```jsx
/////////////RE-rendering in React//////////////////
import React, { useState } from 'react'

function App(){
  const [title,setTitle] = useState("my name is paul");
  function updateTitle(){
    setTitle("my name is" + Math.random());
  }

  return (
    <>
    <button onClick={updateTitle}> Update the title </button>
    <Header title={title} />
    <Header title="my name is harkirat2" />
    <Header title="my name is harkirat3" />
    <Header title="my name is harkirat4" />
    <Header title="my name is harkirat5" />
    <Header title="my name is harkirat6" />
    </>
  )
}

function Header({title}){
  console.log("rendered");
  return <div>
  {title}
  </div>
}
 export default App
```
// this showed us re-rendering of components without re-rendering of the page
## Rerendering only the imp components
Now we will be re-rendering only the important elements
```jsx
//////////////////////re-rendering only the important elements//////////////////////////
import React, { useState } from 'react'

function App(){
  
//<HeaderWithButtons/> will re-render and not the other elements 
//button and the header ----//only re-render
//rest dont need re-render //saving compute


// there was a issue// headerWithButtons didnt worked //camel-casing
  return (
    <>
    <HeaderWithButtons/>
    <Header title="my name is harkirat2" />
    <Header title="my name is harkirat3" />
    </>
  )
}


function HeaderWithButtons(){
  const [title, setTitle] = useState("my name is paul");

  function updateTitle(){
    setTitle("my name is " + Math.random());
  }
  return(
    <>
      <button onClick={updateTitle}> Update the title </button>
      <Header title={title} />
    </>
    )
}

function Header({title}){
  console.log("rendered");
  return <div>
  {title}
  </div>
}

export default App

```

//
While you technically can write functions inside functions in React, it's generally not recommended and considered an anti-pattern for a few reasons:

1. Performance Implications:

- **Re-creation on Every Render:**
    
    Every time the parent component re-renders, the nested function is re-created. This can lead to unnecessary computations and impact performance, especially if the function is complex or interacts with the component's state.
    
- **Memoization Difficulty:**
    
    React's `memo` and `useMemo` hooks are powerful tools for optimizing performance by preventing unnecessary re-renders. However, these optimizations can be harder to implement effectively with nested functions.
    

2. Readability and Maintainability:

- **Increased Complexity:**
    
    Nested functions can make your component code less readable and harder to understand, especially as the complexity of your component grows.
    
- **Debugging Challenges:**
    
    Debugging nested functions can be more challenging than debugging functions defined at the top level.
    
- **Testing Difficulty:**
    
    Writing unit tests for nested functions can be more complicated, as you might need to mock the parent function or access variables within the nested scope.
    

3. Best Practices and Ecosystem:

- **Functional Components:**
    
    React's functional components and hooks encourage a more declarative style of programming. Defining functions at the top level aligns with this style and makes your code easier to reason about.
    
- **Separation of Concerns:**
    
    Defining functions separately promotes a clear separation of concerns, making your code more modular and maintainable.
    

Alternatives to Nested Functions:

- **Helper Functions:**
    
    Define helper functions outside the component that can be reused as needed.
    
- **Custom Hooks:**
    
    If you need to encapsulate complex logic and share it across components, consider creating custom hooks.
    
## react.memo
memo lets you to skip re-rendering of the component if its props are not changed
```jsx
///////////using react.memo to prevent re-rendering
//////////////////////

import React, {memo}, { useState } from 'react'

function App() {
  const [title, setTitle] = useState("my name is paul");
  function updateTitle() {
    setTitle("my name is " + Math.random());
  }

  //by this we are re-rendering the parent component only and not the children
  return (
    <>
      <button onClick={updateTitle}> Update the title </button>
      <Header title={title} />
      <Header title="my name is harkirat2" />
      <Header title="my name is harkirat3" />
      <Header title="my name is harkirat2" />
      <Header title="my name is harkirat3" />
      <Header title="my name is harkirat2" />
      <Header title="my name is harkirat3" />
    </>
  )
}

const Header = memo(function Header({ title }) {
  return <div>
    {title}
  </div>
})

export default App
```

the button , title , parent ----- re-renders
but the multiple children (that didn't changed ) don't re-render
if a parent re-renders all child also re-renders until wrapped inside a react .memo
so what u have wrapped inside a react.memo if that doesn't gets updated the following static children also don't gets updated 
ex-
```jsx
<Header title={title}> 
//here due to memo this child will get updated 

<Header title={title}> 
//but here as the child is static //not updating the state 
//so its will not be re-rendered //skips re-render 
//as the props remains unchanged
```

## Wrapper Components
they take inner react component as an input and renders it 
```jsx

import React, { useState } from 'react'

function App(){
  return <div>
    <CardWrapper innerComponent={<TextComponent />} />
    <CardWrapper innerComponent={<TextComponent2 />} />
  </div>
  // both the components are rendered inside the CardWrapper component
  //both the components are passed as props to the CardWrapper component
}

//this is a wrapper component which will render the inner component inside it
//this is not changing the inner component in any way

function CardWrapper({innerComponent}){
  //create a div which has a border 
  // inside the div render the props

  return <div style={{border:"2px solid black", padding: 20}}>
  {innerComponent}
  </div>
}

function TextComponent(){
  return <div>
  hi there
  </div>
}

function TextComponent2(){
  return <div>
  hi there2
  </div>
}

export default App
```

```jsx
/**
 * Wrapper components Best practices
 */

import React, { useState } from 'react'

//better way to write wrapper components
//Real wrapper

function App(){
  return <div>
  
    <CardWrapper>
    hi there
    </CardWrapper>
    
    <CardWrapper>
    <div>
        hi there
    </div>
    </CardWrapper>
    
    <CardWrapper>
    <TextComponent />
    </CardWrapper>
    
    <CardWrapper>
      <CardWrapper>
        <TextComponent />
      </CardWrapper>
    </CardWrapper>
    
  </div>
}

// ------------this is a nested wrapper component----///////

// here the cardwrapper is the parent component and the cardwrapper inside it is the child component and the textcomponent inside it is the grandchild component[childcomponent of the child component]


//children has every thing inside the <CardWrapper>...</CardWrapper> component
function CardWrapper({children}){
  return <div style={{border:"2px solid black", padding: 20}}>
  {children}
  </div>
}

function TextComponent(){
  return <div>
  hi there
  </div>
}

export default App

```

## To-do app
``` jsx

///////////////////   to-do app  Class notes   ///////////////////////////

//Create a todo app //
// - that takes title, input and description as input 
// - initialize a state array that has 3 todos
// - iterate over array to render all todos
// - a button in the top level app component to add a todo

import React, { memo } from 'react'
import { useState } from 'react'

let counter = 4;//normal js global variable
//used to count the number of todos

export default function App() {

  const[todos , setTodos]= useState([{
    id:1,
    title:"my first todo",
    description:"gym"
  },{
    id:2,
    title:"my second todo",
    description:"study"
  },{
    id:3,
    title:"my third todo",
    description:"eat"
    },{
      id:4,
      title:"my fourth todo",
      description:"fuck and dominate"
    }])

    function addToDo(){
      // // optimal way to write code [using spread operator] // //
      // spreads all the existing todos and add the 4th one at the end
      setTodos([...todos,{
        id:counter++,
        title: Math.random(),
        description: Math.random()
      }])


      //// [uglier code ]////

      // const newTodos = [];
      // for(i=0;i< todos.length; i++){
      //  newTodos.push(todos[i]);
      // }

      // // newTodos = existing todo + 1 // //
      // newTodos.push({
      //   id:4,
      //   title: Math.random(),
      //   description: Math.random()
      // })

      // setTodos(newTodos);
  
    }

  return (
    <>
    <button onClick={addToDo}>Add a ToDo </button>

    {/* // //better approach  using map function to write clean code //  // */}
     {todos.map(todo => <ToDo title={todo.title} description={todo.description} />)}

      
      {/* // // ugly way to code  // // */}      
      {/* 
      {todos.map(function(todo){
      return <ToDo title={todo.title} description={todo.description} />
     })} 
     */}

    </>
  )
}

function ToDo({title,description}){
  return <div>
    <h1>{title}</h1>
    <p>{description}</p>
  </div>
}

```

problem here is that 
Warning: Each child in a list should have a unique "key" prop

key lets react figure out if 
- the todo has been updated 
- if its is deleted 
- it its been added
## React Keys
```jsx
//// Keys in React [todo app] ////## 

import React, { memo } from 'react'
import { useState } from 'react'

let counter = 4 ; //global variable

function App() {

  const [todos, setTodos] = useState([{
    id: 1,
    title: "my first todo",
    description: "gym"
  }, {
    id: 2,
    title: "my second todo",
    description: "study"
  }, {
    id: 3,
    title: "my third todo",
    description: "eat"
  }])

  function addToDo() {
    setTodos([...todos, {
      id: counter++,
      title: Math.random(),
      description: Math.random()
    }])
  }

  return (
    <>
      <button onClick={addToDo}>Add a ToDo </button>
      {todos.map(todo => <ToDo key={todo.id} title={todo.title} description={todo.description} />)}
      //keys are used to uniquely identify the elements in the list and to make the re-rendering faster 
      //keys should be unique
      //especially useful iterating over an array
    </>
  )
}

function ToDo({ title, description }) {
  return <div>
    <h1>{title}</h1>
    <p>{description}</p>
  </div>
}

export default App
```

## **TODO app**

## **React Hooks** 
side effects --->
hooks -- let u use react state and other features without using class
### useEffect
```jsx
import {useState, useEffect} from "react"

export default function App(){
  const [todos, setTodos] = useState([]);

  // remove react.strictmode
  useEffect(() => {
  
    // pit stop 
    fetch("https://sum-server.100xdevs.com/todos")
    .then(async function(res){
      const json = await res.json();
      setTodos(json.todos);
    })
    
  },[])

  return <div>
    {todos.map(todo => <Todo key={todo.id} title={todo.title} description={todo.description}/>)}
  </div>
  
}

function Todo({title, description}){
  return <div>
    <h1>{title}</h1>
    {description}
  </div>
}
```

```jsx

import {useState, useEffect} from "react"

export default function App(){
  // use state
  const [selectedId, setSelectedId] = useState(1);
  
  return <div>
    <button onClick= {
    ()=>{setSelectedId(1)} 
    }>1</button>
    <button onClick= {
      ()=>{setSelectedId(2)} 
      }>2</button>
    <button onClick= {
      ()=>{setSelectedId(3)} 
      }>3</button>
    <button onClick= {
      ()=>{setSelectedId(4)} 
      }>4</button>
    
  <Todo id={selectedId} />
  </div>
  
}

function Todo({id}){
  const [todo, setTodo] = useState({});

  // use effect hook
  useEffect(()=>{
    fetch(`https://sum-server.100xdevs.com/todo?id=${id}`)
    .then(async function(res){
      const json = await res.json();
      setTodo(json.todo);
    })
  },[id])
  // if u dont use the id as a dependency
  // fetch will run once only once 
  //and although the id inside App changes it will not produce effect in Todo
  
 return <div>
   Id:{id}
    <h1>{todo.title}</h1>
    {todo.description}
  </div>
}


```


### useMemo
useMemo is used to memorize a value. 
This is useful when you have a computationally expensive calculation that you don't want to re-run on every render unless specific dependencies change.
```jsx
import { useState, useEffect, useMemo } from "react";

function App() {
  const [counter, setCounter] = useState(0);
  const [inputValue, setInputValue] = useState(1);


  //problem with this is clicking on the button will change the state of the counter leading to rerendering the whole component and running the for looop again
  // let count = 0;
  // for (let i = 1; i <= inputValue; i++) {
  //   count = count + i;
  // }

  
  //another approach use Effect hook  //decent
  // only when the input value changes the useEffect will run
  //problem u are causing an unnecesery rerendering on changing inputValue
  // const[finalValue, setFinalValue] = useState(0);
  // useEffect(()=>{
  //   let count = 0;
  //   for (let i = 1; i <= inputValue; i++) {
  //     count = count + i;
  //   }
  //   setFinalValue(count);
  // },[inputValue])


  //useMemo hook
  // just this saves an extra state render 
  let count = useMemo(()=>{
    let finalCount = 0;
    for (let i = 1; i <= inputValue; i++) {
        finalCount = finalCount + i;
    }
    return finalCount;
  },[inputValue]);
  

  return <div>
    <input onChange={function(e) {
    // console.log(e.target.value)// this is the data inside the input box
      setInputValue(e.target.value);
    //ie now inputValue = setInputValue(e.target.value)
    }} placeholder={"Find sum from 1 to n"}></input>
    <br />
    Sum from 1 to {inputValue} is {count}
    {/* Sum from 1 to {inputValue} is {finalValue}  */}
    {/*  during using effect hook  */}
    <br />
    <button onClick={() => {
      setCounter(counter + 1);
    }}>Counter ({counter})</button>
  </div>
}

export default App;
```

### useCallback
useCallback is used to memorize a callback function.
This is useful when you have a function that you pass down to child components and you don't want to re-create the function on every render, which could lead to
unnecessary re-renders of the child components.
```jsx
import {memo, useState, useEffect, useMemo, useCallback } from "react";

function App() {
  const [counter, setCounter] = useState(0);

    // var a = 1;    

  // function a() {
  //   console.log("hi there ")
  // };

  const a = useCallback(() => {
    console.log("hi there");
  },[])

  return <div>
  <button onClick = {() => {
    setCounter(counter + 1)
  }}>Counter ({counter})</button>
    <Demo a={a} />
  </div>
}

// memo func  //ie not will not change unless the value of a changes

// here inside the app 
//   <Demo a={a} />
// the values of a are equal 
// although they are refferentially diff

//now if we use a func instead of var a in the func
// the value of a will change as the func are not equal
// even though the function doesnt changes but refferentially it changes 
const Demo = memo(({a}) =>{
  console.log("render demo");
  return <div>
  Hi there 
  </div>
})

export default App;
```

Assignment 
```jsx
import { memo, useState } from "react";

function App() {
  const [count, setCount] = useState(0)

  function logSomething() {
    console.log("child clicked")
  }

  return <div>
    <ButtonComponent inputFunction={logSomething} />
    <button onClick={() => {
      setCount(count + 1);
    }}>Click me {count}</button>
  </div>
}

// ButtonComponent is a child component
const ButtonComponent = memo(({inputFunction}) => {
  console.log("child render")

  return <div>
    <button onClick={inputFunction}>Button clicked</button>
  </div>
})

export default App;
```

### useRef
useRef is a hook in React that is used to persist values across renders without causing a re-render of the component. It's often used for accessing DOM elements directly, storing a mutable reference to a value, or keeping track of a previous state/value. 

```jsx

```


### Custom Hooks
the function inside of which u define a hook must be a function or a raw component 
```jsx
// WRONG Approach 

import { useState } from "react";

function App() {
  const [todos, setTodos] = useState([])

    useEffect(() => {  
    fetch("https://sum-server.100xdevs.com/todos")
    .then(async function(res){
      const json = await res.json();
      setTodos(json.todos);
    })    
  },[todos])

  return <div>
  {todos.map(todo => <Todo key={todo.id} title={todo.title} description={title.description} />)}
  </div>
}
function Todo({title,description}){
return <div>
<h1>
{title}
</h1>
<h4>
{description}
</h4>
</div>
}

export default App;

```

```jsx 
//right approach

import { useState } from "react";

function useTodos(){
  const [todos, setTodos] = useState([]);
    useEffect(() => {  
    fetch("https://sum-server.100xdevs.com/todos")
    .then(async function(res){
      const json = await res.json();
      setTodos(json.todos);
    })    
  },[todos])

return todos;
}

funct
Routing in React
```jsx
function App(){

  return (
    <div>
    <div style={{background:"black", color:"white"}}>
    {/* creating a topbar that remain consistent irrespective of app  content changes*/}
    Hi i was here 
    </div>
      <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/dashboard" element={<Dashboard />} />
      </Routes>
      </BrowserRouter>
    </div>
  )
}
```

why window.location.href method is bad ?
- it re-renders the whole site leading to client bundle to again rerender in the client server 
- it dont use CSR client side routing instead rerenders the whole site 

using navigate uses CSR preventing the site to rerender again 
### useNavigate Hook 
```jsx
import {BrowserRouter, Routes, Route, useNavigate } from "react-router-dom"
import {Dashboard} from "./compoenets/dashboard"
import {Landing} from "./compoenets/landing"

export default function App(){
  const navigate = useNavigate();
  function handleClick(){
    navigate("/about")
  }
  return(
    <div>
     <div>
     <button onClick={()=>{
      // window.location.href = "/"    //bad approach
      navigate("/");
     }}>Landing Page</button>
      <button onClick={()=>{
    // window.location.href = "/Dashboard"    //bad approach
      naivgate("/Dashboard")
         }}>Dashboard</button>
     </div>
        <BrowserRouter>
        <Routes>
          <Route path="/" element={<Landing />} />
          <Route path="/dashboard" element={<Dashboard />} />
        </Routes>
        </BrowserRouter>
      </div>
  )
}
```
this is  bugged
useNavigate hook whenever is being used is expected to be used inside the browserRouter 
```jsx
import {BrowserRouter, Routes, Route, useNavigate } from "react-router-dom"
import {Dashboard} from "./compoenets/dashboard"
import {Landing} from "./compoenets/landing"

export default function App(){
  function handleClick(){
    navigate("/about")
  }
  return(
    <div>
      <BrowserRouter>
          <Appbar />
        <Routes>
          <Route path="/" element={<Landing />} />
          <Route path="/dashboard" element={<Dashboard />} />
        </Routes>
        </BrowserRouter>
      </div>
  )
}

function Appbar(){
  const navigate = useNavigate();

  return <div>
    <div>
       <button onClick={()=>{
        navigate("/");
       }}>Landing Page</button>
        <button onClick={()=>{
        naivgate("/Dashboard")
           }}>Dashboard</button>
    </div>
  </div>
}
```

Suspense Api 
is used when we have to use async components ,async datafetching,etc
which is async and is not rendered immeadiately
```jsx
import React,{lazy, Suspense} from 'react'
import {BrowserRouter, Routes, Route, useNavigate } from "react-router-dom"

// const Dashboard = React.lazy(()=>'./compoenets/dashboard')
const Dashboard = lazy(()=>'./compoenets/dashboard')

const Landing = lazy(()=>'./compoenets/landing')

// Suspense Api
export default function App(){
  return(
    <div>
      <BrowserRouter>
          <Appbar />
        <Routes>
          <Route path="/" element={<Suspense fallback=("loading...")><Landing /></Suspense> } />
          <Route path="/dashboard" element={<Suspense fallback=("loading...")><Dashboard /></Suspense>} />
        </Routes>
        </BrowserRouter>
    </div>
  )
}

function Appbar(){
  const navigate = useNavigate();

  return <div>
    <div>
       <button onClick={()=>{
        navigate("/");
       }}>Landing Page</button>
        <button onClick={()=>{
        naivgate("/Dashboard")
           }}>Dashboard</button>
    </div>
  </div>
}
```

## **Prop Driling**
https://react.dev/learn/passing-data-deeply-with-context

u need to drill prop down the compenent tree
- makes it hard to maintain and unreadable

the problem with passing props -\
- inconvenient to pass props down the tree to child elements 
- the nearest common ancestor could be far remove from the component that need data ,and lifting the prop much high in the  table can lead to --prop drilling
```jsx
import {useState} from 'react'

export default function App(){
   const [count , setCount] = useState(0);

  return (
    <div>
    <Count count={count} />
    <Buttons count={count}  setCount={setCount}/>
    </div>
  )
}

function Count({count}){
  return <div>
    {count}
  </div>
  
}

function Buttons({count, setCount}){
  return <div>
  <button onClick={()=>{
    setCount(count+1)
  }}>increment</button>
  <button onClick={()=>{
      setCount(count-1)
    }}>decrement</button>
  </div>
}

```

So in this code if we need to use button component inside the Count we need to pass the props needed in Buttons component
```jsx

function Count({count}){
  return <div>
    {count,setCount}
    <Buttons count={count}  setCount={setCount}/>
  </div>
}
```

## **Context API**
https://react.dev/learn/passing-data-deeply-with-context
if u are using context api you are pushing ur state management outside the core react component
```jsx
// /src/context.js

import {createContext } from 'react'

//create context variable to teleport accross various components
export const Context = createContext(0);
```

```jsx
// /src/App.jsx

import {useState, useContext} from 'react'
import Context from "./src/context.jsx"


export default function App(){
   const [count , setCount] = useState(0);

  // wrap anyone who wants to use the teleported value inside a provider 
  //  <Context.Provider value={count}>
  // here we are teleporting the count prop 

  return (
    <div>
      <Context.Provider value={count}>
    <Count  setCount={setCount} />
      </Context.Provider>
    </div>
  )
}

function Count({setCount}){
// /src/App.jsx

import {useState, useContext} from 'react'
import Context from "./src/context.jsx"


export default function App(){
   const [count , setCount] = useState(0);

  // wrap anyone who wants to use the teleported value inside a provider 
  //  <Context.Provider value={count}>
  // here we are teleporting the count prop 

  return (
    <div>
      <Context.Provider value={count}>
    <Count  setCount={setCount} />
      </Context.Provider>
    </div>
  )
}

function Count({setCount}){
  return <div>
    <CountRenderer/>
    <Buttons setCount={setCount}/>
  </div>
}

function CountRenderer(){
  const count = useContext(CountContext);
  return <div>
    {count}
  </div>
}

function Buttons({setCount}){
  const count = useContext(CountContext);
  return <div>
  <button onClick={()=>{
    setCount(count+1)
  }}>increment</button>
  <button onClick={()=>{
      setCount(count-1)
    }}>decrement</button>
  </div>
}// /src/App.jsx

import {useState, useContext} from 'react'
import Context from "./src/context.jsx"


export default function App(){
   const [count , setCount] = useState(0);

  // wrap anyone who wants to use the teleported value inside a provider 
  //  <Context.Provider value={count}>
  // here we are teleporting the count prop 

  return (
    <div>
      <Context.Provider value={count}>
    <Count setCount={setCount} />
      </Context.Provider>
    </div>
  )
}

function Count({setCount}){
//console.log("count re-rendered")
  return <div>
    <CountRenderer/>
    <Buttons setCount={setCount}/>
  </div>
}

function CountRenderer(){
  const count = useContext(CountContext);
  return <div>
    {count}
  </div>
}

function Buttons({setCount}){
  const count = useContext(CountContext);
  return <div>
  <button onClick={()=>{
    setCount(count+1)
  }}>increment</button>
  <button onClick={()=>{
      setCount(count-1)
    }}>decrement</button>
  </div>
}

```


---------------------------------------------------------
similarly if we want to teleport setCount ,count or even more props to children elements 
```jsx
// /src/context.js

import {createContext } from 'react'

export const Context = createContext({
	count ,setCount
});
```

```jsx
// in App.jsx

//...
      <Context.Provider value={count, setCount}>
//...
```

#### issue with context api
event components that not using props are also being re-rendered 
it is to make syntax more cleaner
not to make the application more performant
So we use state management library like react 


## Recoil
