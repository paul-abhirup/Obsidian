# CSS from Cohort

common styling attributes - 
- font-size
- color  
	  - gives font colour to the text
- background
	  - gives bacground colour to the element
- border-radius
	  - rounded border shapes
- border
	  - this tells how the border is 
	    border: 1px solid black // gives a solid black border
	    border: 1px dotted black // gives a dotted black border
- padding 
		- space from the top or bottom; // inside the div
		- 
- margin
	  - space added outside the div
	    margin: 50px;
	    // means outside the div element 50px will be added to the top to the right, left , bottom
- box-shadow
	  - gives shadow to the box element

Example of the code --
```css
<h1 style= "
font-size: 100px;
color: red;
background: aqua; 
border-radius: 10px; 
padding: 10px; 
margin: 20px;
box-shadow: 2px 10px 10px black;
">
hi there ;
</h1>
```

### How to position?
divs takes up all the space available horizontally
span only takes up as much space as needed

now how to make divs take up only the space they need?

previously we position elements by using padding or margin something like that  
padding-left = 10px
padding-right = 20 px
	
	// padding is inside the div 
	// margin is outside the div

Also use some thing like float in CSS
	`<span>Zerodha</span>`
	`<span style="float: right" > Sign up </span>`
So here inside the div that 2 span elemets are seperated

This is dumb way of doing things ? 
becuase you cant control the spacing and many more customization we use this models
 many more methods include 
	 - abolute postioning
	 - floats

this is the optimum ways so we use **FlexBox

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Hello, World!</title>
    <link rel="stylesheet" href="styles.css" />
  </head>
  <body>
      <div style="display: flex; justify-content: space-between; margin-left: 100px; margin-right: 100px;">
        <div style="padding-top: -30px">
          <h1><b>Zerodha</b></h1>
        </div>
        <div style="display: flex; ">
          <div style="padding: 20px; ">
            Sign Up
          </div>
          <div style="padding: 20px;" >
            About Us
          </div>
          <div style="padding: 20px;" >
            Products
          </div>
          <div style="padding: 20px;">
            Pricing
          </div>
        </div>
      </div>
  </body>
</html>
```

---
---