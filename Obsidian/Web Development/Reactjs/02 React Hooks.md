side effects 
hooks -- let u use react state and other features without using class

# useEffect
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


# useMemo
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

# useCallback
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


# Custom Hooks
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

### right  approach 
```jsx 
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

function App() {
   const todos = useTodos();
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

#  useRef
useRef is a hook in React that is used to persist values across renders without causing a re-render of the component. It's often used for accessing DOM elements directly, storing a mutable reference to a value, or keeping track of a previous state/value. 

```jsx

```

# Custom Hooks

