
things to know for frontend styling 
- flex
- grid
- responsiveness
- background colour, hover
- fonts, font colour

divs always takes up all the horizontal space, 
spans only takes up as much space as needed,
so, to make div take only the space needed we use the flexbox model
### **flexbox  model**
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

grid where elements are of equal widths
```tsx
//this means the grid have 3 elements 
//so each element will be of 100/3 = 33.33%
<div className='grid grid-cols-3' >
        <div className='bg-red-600'>hello</div>
        <div className='bg-blue-600'>hello</div>
        <div className='bg-green-600'>hello</div>
</div>
```

```tsx
//grid has 5 elements each of 20%
 <div className='grid grid-cols-5' >
        <div className='bg-red-600'>hello</div>
        <div className='bg-blue-600'>hello</div>
        <div className='bg-green-600'>hello</div>
        <div className='bg-purple-600'>hello</div>
        <div className='bg-pink-300'>hello</div>
      </div>
```

grids where elements are of unequal widths
```tsx
//here we divide the grid into 10 columns and then assign no of columns to each element
 <div className='grid grid-cols-10' >
        <div className='bg-red-600 col-span-4'>hello</div>
        <div className='bg-blue-600 col-span-4'>hello</div>
        <div className='bg-green-600 col-span-2'>hello</div>
      </div>
```

### Responsiveness
understanding breakpoints 
sm -- 640px
md -- 768px
lg -- 1024px
xl -- 1280px

so basically after this breakpoints the site changes 

tailwind uses mobile first-approach
' unpreffixed utilities takes effect in all screen sizes but preffixed utilities only effect specific breakpoints and above'

```tsx
<div className='bg-red-500 sm:bg-pink-300'>
      Hello there
     </div>
```
so by default it is red but as the display increases above sm: 640px then it is pink
dont think of that you are building for mobile screen, instead think of that after this breakpoint it changes to this

```tsx
<div className='grid grid-cols-1 md:grid-cols-3' >
        <div className='bg-red-600 '>hello</div>
        <div className='bg-blue-600 '>hello</div>
        <div className='bg-green-600 '>hello</div>
      </div>
```

### Colour system in Tailwind
reffer tailwind colour pallet
shades of colour

Font and background colour
```tsx
<div className='bg-red-500 text-yellow-500' >
        Hello HI 
      </div>
```

### Font size 
text-xs
text-sm
text-base
text-lg
text-xs

### Border radius
rounded-s-md
rounded-s-lg
rounded-s-xl

Tailwind icons 
- HeroIcons  --- to add icons in tailwind css

colour picking from figma design
inside tailwind.config
```jsx
theme: {
    extend: {
      colors: {
        blue:{
          700: "#146eb4"
        }
      }
    },
  },
```