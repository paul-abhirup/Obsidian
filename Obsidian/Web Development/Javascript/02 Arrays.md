```jsx

// Array:   push(), pop(), shift(), unshift(), splice(), slice(), concat(), forEach(), map(), filter(), reduce(), find(), sort()

// push()
function pushExample(arr, element) {
  arr.push(element);
  console.log("After push:", arr);
}
pushExample([1, 2, 3], 4);


// pop()
function popExample(arr) {
  arr.pop();
  console.log("After pop:", arr);
}
popExample([1, 2, 3]);



// shift()
function shiftExample(arr) {
  arr.shift();
  console.log("After shift:", arr);
}
shiftExample([1, 2, 3]);



// unshift()
function unshiftExample(arr, element) {
  arr.unshift(element);
  console.log("After unshift:", arr);
}
unshiftExample([1, 2, 3], 0);



// concat()
function concatExample(arr1, arr2) {
  let arr3 = arr1.concat(arr2);
  console.log("After concat:", arr3);
}
concatExample([1, 2, 3], [4, 5, 6]);



// forEach()
function forEachExample(arr) {
  arr.forEach(function(item, index) {
    console.log(item, index);
  });
}
forEachExample([1, 2, 3]);



// map()
function mapExample(arr) {
  let newArr = arr.map(function(item) {
    return item * 2;
  });
  console.log("After map:", newArr);
}
mapExample([1, 2, 3]);



// filter()
function filterExample(arr) {
  let newArr = arr.filter(function(item) {
    return item > 3;
  });
  console.log("After filter:", newArr);
}
filterExample([1, 2, 3, 4, 5]);



// find()
function findExample(arr) {
  let found = arr.find(function(item) {
    return item > 3;
  });
  console.log("After find:", found);
}
findExample([1, 2, 3, 4, 5]);



// sort()
function sortExample(arr) {
  arr.sort(function(a, b) {
    return a - b;
  });
  console.log("After sort:", arr);
}
sortExample([5, 2, 3, 4, 1]);

```