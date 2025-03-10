
things to know for frontend styling 
- flex
- grid
- responsiveness
- background colour, hover
- fonts, font colour

divs always takes up all the horizontal space, 
spans only takes up as much space as needed,
so, to make div take only the space needed we use the flexbox model

## Adding Tailwind in a Project
Mostly in the doc whatever it says
and follow the configuration

Like for the class project we are adding a tailwind to the  Vite-React Project 
- create a react app using vite 
		`npm create vite@latest my-app`
- add tailwind in it 
	https://tailwindcss.com/docs/installation/using-vite

## **Flexbox  model**
postion elements(specially divs) right next to each other 
? because postioning divs is problem in normal css

justifyContent ---> how they should be placed

`justifyContent: "space-between"`

| Flex          |                                                |
| ------------- | ---------------------------------------------- |
| flex-start    | postion elements next to each other from start |
| flex-end      | elements next to each other from end           |
| center        | placing things from center                     |
| space-between | equal space between each element               |
| space-around  | create a space padding around each element     |


in react app
```jsx
function App(){
return(
	<>
		<div style={{display: 'flex', justifyContent:"center"}} >
	      <div style={{backgroundColor: 'red'}}>hello</div>
	      <div style={{backgroundColor: 'blue'}}>hello</div>
	      <div style={{backgroundColor: 'green'}}>hello</div>
	      <div style={{backgroundColor: 'yellow'}}>hello</div>
		</div>
	</>
  )
}
```

with tailwind
```jsx
<div className='flex justify-center' >
        <div className='bg-red-600'>hello</div>
        <div className='bg-blue-600'>hello</div>
        <div className='bg-green-600'>hello</div>
</div>
```

## **Grids**

#### Equal widths
using grid where elements are of equal width
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

### Unequal widths
usging grid where elements are of unequal width
```tsx
//here we divide the grid into 10 columns and then assign no of columns to each element
 <div className='grid grid-cols-10' >
        <div className='bg-red-600 col-span-4'>hello</div>
        <div className='bg-blue-600 col-span-4'>hello</div>
        <div className='bg-green-600 col-span-2'>hello</div>
      </div>
```

## When to use Grids and flexbox ??


## Responsiveness
understanding breakpoints 
sm -- 640px
md -- 768px
lg -- 1024px
xl -- 1280px

so basically after this breakpoints the site changes 
Laptop ---> 1440 px
Desktop --> 1440 px
Mobile ---> 480 px
Mobile LAndsacpe ----> 768 px
Tablet --> 834 px
Tablet LAndscape ---> 1024 px

tailwind uses mobile first-approach
### ` unpreffixed utilities takes effect in all screen sizes but preffixed utilities only effect specific breakpoints and above `

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

Common Device breakpoint


### Colour system in Tailwind
reffer tailwind colour pallet
https://tailwindcss.com/docs/colors
for the different colour shades

Font and background colour
```tsx
<div className='bg-red-500 text-yellow-500' >
        Hello HI !!!
      </div>
```

### Font size 
text-xs
text-sm
text-base
text-lg
text-xl
text-2xl

### Border radius
https://tailwindcss.com/docs/border-radius

rounded-s-md
rounded-s-lg
rounded-s-xl

Tailwind icons 
**HeroIcons**  --- to add icons in tailwind css

colour picking from figma design
So baiccally when you want to create custom colours

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


## Building the UI for dukkan

Figma file --> https://www.figma.com/design/1QTpfgcJLng3SEHv3V7Nr4/Payouts-V2---2023



