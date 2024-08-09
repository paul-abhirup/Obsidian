things to know for frontend styling 
- flex
- grid
- responsiveness
- background colour, hover
- fonts, font colour

### **flexbox**
postion elements(specially divs ) right next to each other 
justifyContent: "space-between"
justifyContent ---> how they should be placed 
space between ---> equal space between the divs
flex-start -> postion elements next to each other from start
flex-end -> elements next to each other from end
center --> placing things from center
space-between -> equal space between each element
space-around -> create a space padding around each element

in react app
```jsx
<div style={{display: 'flex', justifyContent:"center"}} >
      <div style={{backgroundColor: 'red'}}>hello</div>
      <div style={{backgroundColor: 'blue'}}>hello</div>
      <div style={{backgroundColor: 'green'}}>hello</div>
      <div style={{backgroundColor: 'yellow'}}>hello</div>
</div>
```
with tailwind
```jsx
<div className='flex justify-center' >
        <div className='bg-red-600'>hello</div>
        <div className='bg-blue-600'>hello</div>
        <div className='bg-green-600'>hello</div>
</div>
```

### **grids**
