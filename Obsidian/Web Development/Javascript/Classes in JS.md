#### Classes

In JavaScript, classes are a way to define blueprints for creating objects (these objects are different from the objects datatype).

```js
class Rectangle {
   constructor(width, height, color) {
	    this.width = width;
	    this.height = height;
	    this.color = color; 
   }
   
   area() {
	   const area = this.width * this.height;
		 return area;
   }
   
   paint() {
			console.log(`Painting with color ${this.color}`);
   }
   
}

const rect = new Rectangle(2, 4);
const area = rect.area();
console.log(area)
```

Key Concepts
- Class Declaration:
	- Inside a class, you define properties (variables) and methods (functions) that will belong to the objects created from this class.
- Constructor:
	- A special method inside the class that is called when you create an instance (an object) of the class.
	- It’s used to initialize the properties of the object.
- Methods:
	- Functions that are defined inside the class and can be used by all instances of the class.
- Inheritance:
	- Classes can inherit properties and methods from other classes, allowing you to create a new class based on an existing one.
- Static Methods:
	- Methods that belong to the class itself, not to instances of the class. You call them directly on the class.
- Getters and Setters:
	- Special methods that allow you to define how properties are accessed and modified.
- new Keyword
	-  The new keyword creates a new empty object(instance), with a type of object.
	- The new keyword sets the internal prototype property of the constructing function.
	- The new keyword binds this variable to the newly created object and returns it .

# Inheritance in classes

Inheritance in JavaScript classes allows one class to inherit properties and methods from another class. 

Creating a Base Class
```js
class Shape {
    constructor(color) {
        this.color = color;
    }

    paint() {
			console.log(`Painting with color ${this.color}`);
    }

    area() {
        throw new Error('The area method must be implemented in the subclass');
    }

    getDescription() {
        return `A shape with color ${this.color}`;
    }
}
```

Creating a Rectangle Class from Base class; with additonal properties
```js
class Rectangle extends Shape {
    constructor(width, height, color) {
        super(color);  // Call the parent class constructor to set the color
        this.width = width;
        this.height = height;
    }

    area() {
        return this.width * this.height;
    }

    getDescription() {
        return `A rectangle with width ${this.width}, height ${this.height}, and color ${this.color}`;
    }
}
```

Calling rectangle class
```js
const Rectangle1 = new Rectangle(10,20,"red");
console.log(Rectangle1.area());
console.log(Rectangle1.paint());
console.log(Rectangle1.getDescription());
```



