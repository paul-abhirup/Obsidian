[recoil](https://www.youtube.com/watch?v=_ISAA_Jt9kI) video

recoil ----
- uses the concept of the atom to store the state
- atom can be defiined outside the component
- can be teleported to any component

its a good practice to create a folder src/store/atoms and there store the atom components for state management
```jsx
// /src/store/atoms/count.jsx
import { atom } from "recoil";

export const countAtom = atom({
key: "countAtom",
default: 0
});
```

```jsx
import { useContext, useMemo, useState } from "react"
import { RecoilRoot, useRecoilState, useRecoilValue, useSetRecoilState } from "recoil";
import { countAtom } from "./store/atoms/count";

function App() {
  return (
    <div>
      <RecoilRoot>
        <Count />
      </RecoilRoot>
    </div>
  )
}

function Count() {
  console.log("re-render");
  return <div>
    <CountRenderer />
    <Buttons />
  </div>
}

function CountRenderer() {
  const count = useRecoilValue(countAtom);

  return <div>
    <b>
      {count}
    </b>
  </div>
}

function Buttons() {
  // const [count, setCount] = useRecoilState(countAtom); 
  // its not a good practice to use setCount in the same component where we are using countAtom


  //button dont really need count as a state, they just need to update the count
  //it doesnt need to show it in the UI


  //ways to manipulate state 
  //setCount(count + 1)   //where the count need to  be passed as a parameter
  //setCount(count => count + 1)  //where the count is a function that returns the new value

  // console.log("buttons re-rendererd");


  const setCount = useSetRecoilState(countAtom);

  return <div>
    <button onClick={() => {
      //setCount(count + 1)
      setCount(count => count + 1)
    }}>Increase</button>

    <button onClick={() => {
      setCount(count => count - 1)
    }}>Decrease</button>
  </div>
}

export default App

```


### Assignment - 
render " it is even " when the current value is even
```jsx
import { atom, selector } from "recoil";

export const countAtom = atom({
    key: "countAtom",
    default: 0
});


export const evenSelector = selector({
    key: "evenSelector",
    get: ({ get }) => {
        const count = get(countAtom);
        return count % 2;
    }
});

```

```jsx
import { useContext, useMemo, useState } from "react"
import { RecoilRoot, useRecoilState, useRecoilValue, useSetRecoilState } from "recoil";
import { countAtom, evenSelector } from "./store/atoms/count";

function App() {
  return (
    <div>
      <RecoilRoot>
        <Count />
      </RecoilRoot>
    </div>
  )
}

function Count() {
  console.log("re-render");
  return <div>
    <CountRenderer />
    <Buttons />
  </div>
}

function CountRenderer() {
  const count = useRecoilValue(countAtom);

  return <div>
    <b>
      {count}
    </b>
    <EvenCountRenderer />
  </div>
}

//ugly way to do it
// function EvenCountRenderer() {
//   const count = useRecoilValue(countAtom);
//   return <div>
//     {count % 2 === 0 ? "It is even" : null}
//   </div>
// }


//better approach to do it
// function EvenCountRenderer() {
//   const isEven = useMemo(() => {
//     return count % 2 === 0
//   }, [count]);

//   return <div>
//     {isEven ? "It is even" : null}
//   </div>
// }
//it only changes when the count changes
//if a rerender happen and count is the same, it will not recompute the value



function EvenCountRenderer() {
  const isEven = useRecoilValue(evenSelector);

  return <div>
    {isEven ? "It is even" : null}
  </div>
}

function Buttons() {
  // const [count, setCount] = useRecoilState(countAtom); 
  // its not a good practice to use setCount in the same component where we are using countAtom

  //button dont really need count as a state, they just need to update the count
  //it doesnt need to show it in the UI

  //ways to manipulate state 
  //setCount(count + 1)   //where the count need to  be passed as a parameter
  //setCount(count => count + 1)  //where the count is a function that returns the new value

  // console.log("buttons re-rendererd");

  const setCount = useSetRecoilState(countAtom);

  return <div>
    <button onClick={() => {
      //setCount(count + 1)
      setCount(count => count + 1)
    }}>Increase</button>

    <button onClick={() => {
      // setCount(count - 1)
      setCount(count => count - 1)
    }}>Decrease</button>
  </div>
}

export default App

```

