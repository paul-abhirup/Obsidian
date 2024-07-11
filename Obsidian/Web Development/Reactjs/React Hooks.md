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
