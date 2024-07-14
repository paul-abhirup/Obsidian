
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

useNavigate Hook 
```jsx
import {useNavigate } from "react"

export default function App(){
  const navigate = useNavigate();
  function handleClick(){
    navigate("/about")
  }
  return(
    <div>
      <h1>App</h1>
      <button onClick={handleClick}>About</button>
    </div>
  )
}

```
