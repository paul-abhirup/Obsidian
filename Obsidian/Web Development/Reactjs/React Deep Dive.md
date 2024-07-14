## React-Returns

create a react app that has a header component 
- that take title as a prop and renders it inside a div
- App renders more than 1 Header 
```jsx
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
	//is returning multiple children component
	//this helps in returning multiple children

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
```jsx
/////////////RE-rendering in React//////////////////
import React, { useState } from 'react'


function App(){
  const [title,setTitle] = useState("my name is paul");
  function updateTitle(){
    setTitle("my name is " + Math.random());
    // Math.random() will generate a random number between 0 and 1
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
  // every time a parent re-renders all the children re-render as well. 
  //so its important to render only the important elements and not all of them
}

function Header({title}){
  console.log("rendered");
  return <div>
  {title}
  </div>
}
 export default App

```

```jsx
//////////////////////re-rendering only the important elements//////////////////////////
import React, { useState } from 'react'

function App(){
  
  // by this we are rendering only the important elements
  //now only the <HeaderWithButtons/> will re-render and not the other elements 

  return (
    <>
    <HeaderWithButtons/>
    <Header title="my name is harkirat2" />
    <Header title="my name is harkirat3" />
    </>
  )
}

//this contains the components that require re-render 
//button and the header
//rest dont need rerender //saving compute
function HeaderWithButtons(){
  const [title, setTitle] = useState("my name is paul");

  function updateTitle() {
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

## react.memo
```jsx
///////////using react.memo to prevent re-rendering
//////////////////////
//memo lets you to skip re-rendering of the component if its props are not changed

import React, {memo} from 'react'
import { useState } from 'react'

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
but he multiple children (that didn't changed ) don't re-render
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


//create a todo app //
- that takes title,input and description as input 
- initialize a state array that has 3 todos 
- iterate over array to render all todos 
- a button in the top level app component to add a todo 
## to-do app
```jsx


///////////////////   to-do app  Class notes   ///////////////////////////


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
//// Keys in React [todo app] ////

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

```jsx
class NavBasic extends React.PureComponent{
  static defaultProps = {
    onBack: null 
  };

  //these are life cycle events 
  //they used in understanding which components are being rendered
  onComponentMount(){
  }

  onComponentUnMount(){
  }

  onRender(){    
  }
  
  render(){
    return(
      <div>
        
      </div>
    )
  }
  
}
```