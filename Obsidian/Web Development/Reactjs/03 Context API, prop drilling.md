
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
\
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

## [Prop Driling](https://react.dev/learn/passing-data-deeply-with-context)
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

# Context API
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