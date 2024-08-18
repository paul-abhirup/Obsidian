#js #javascript #webDevelopment

```js

str.replace(target, replacement)

str.split(separator)
//splits the string from the seperator
/*
splitString("HelloWWorld", "W");
After split: [ 'Hello', '', 'orld' ]
*/


str.IndexOf(target)  
//we need 2 argument : str , target 
// target may be a word or a letter as both are : string

str.lastIndexOf(target)
//ex -- findIndexOf("Hello World World", "World") = 12

str.slice(start,end)
//slices thr str and serves the slice 

str.substring(start, end) 
//similar to slice function

```



```js
// String: length, indexOf(), lastIndexOf(), slice(), substring(), replace(),split(), trim(), toUpperCase(), toLowerCase(), etc.


// Length
function getLength(str) {
  console.log("Length:", str.length);
}
getLength("Hello World");


// indexOf
function findIndexOf(str, target) {
  console.log("Index:", str.indexOf(target));
}
findIndexOf("Hello World", "World");
//even the whole word is being counted as a letter due to string


// lastIndexOf
function findLastIndexOf(str, target) {
  console.log("Index:", str.lastIndexOf(target));
}
findLastIndexOf("Hello World World", "World");
//if index is -1

// slice
function getSlice(str, start, end) {
  console.log("After slice:", str.slice(start, end));
}
getSlice("Hello World", 0, 5);
getSlice("Hello World", 0, -1);//is like 1 element from the last position
getSlice("Hello World", 0, 0);//returns nothing 

// substring
function getSubstring(str, start, end) {
  console.log("After substring:", str.substring(start, end));
}
getSubstring("Hello World", 0, 5);

// replace
function replaceString(str, target, replacement) {
  console.log("After replace:", str.replace(target, replacement));
}
replaceString("Hello World", "World", "JavaScript");

// split
function splitString(str, separator) {
  console.log("After split:", str.split(separator));
}
splitString("Hello World", " ");

// trim
function trimString(str) {
  console.log("After trim:", str.trim());
}
trimString(" Hello World ");

// toUpperCase
function toUpper(str) {
  console.log("After toUpperCase:", str.toUpperCase());
}
toUpper("Hello World");

// toLowerCase
function toLower(str) {
  console.log("After toLowerCase:", str.toLowerCase());
}
toLower("Hello World");

//join


```
#  slice vs string
**What they have in common:**

1. If `start` equals `stop`: returns an empty string
2. If `stop` is omitted: extracts characters to the end of the string
3. If either argument is greater than the string's length, the string's length will be used instead.

**Distinctions of** [`substring()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/substring)**:**

1. If `start > stop`, then `substring` will swap those 2 arguments.
2. If either argument is negative or is `NaN`, it is treated as if it were `0`.

**Distinctions of** [`slice()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/slice)**:**

1. If `start > stop`, `slice()` will return the empty string. (`""`)
2. If `start` is negative: sets char from the end of string, exactly like `substr()` in Firefox. This behavior is observed in both Firefox and IE.
3. If `stop` is negative: sets stop to: `string.length – Math.abs(stop)` (original value), except bounded at 0 (thus, `Math.max(0, string.length + stop)`) as covered in the [ECMA specification](https://www.ecma-international.org/ecma-262/9.0/index.html#sec-string.prototype.slice).

