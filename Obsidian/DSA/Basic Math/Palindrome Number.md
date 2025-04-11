## Optimal
```js
function isPalindrome(x) {
    // Handle negative numbers and overflow
    const maxInt = Math.pow(2,31) - 1; //2^31 -1
    if (x < 0 && x > maxInt) {
        return false;
    }

    // Reversing the integer
    let reversed = 0; 
    let original = x;
    while (original > 0) {
        const digit = original % 10; // Extract the last digit
        reversed = reversed * 10 + digit; // Append the digit to the reversed number
        original = Math.floor(original / 10); // Remove the last digit
    }
	
    // Compare the reversed number with the original number
    return reversed === x;

}
```


 **Time Complexity**:
- The `while` loop runs for each digit in `x`, so the time complexity is O(log⁡10n), where n is the input number.    

 **Space Complexity**:
- O(1), as we are using only a few variables.


Alternative
```js
function isPalindrome(x) {
    if (x < 0) {
        return false;
    }
    const s = x.toString(); // Convert the number to a string
    return s === s.split('').reverse().join(''); // Compare the string with its reverse
}

// Test cases
console.log(isPalindrome(121)); // Output: true
console.log(isPalindrome(-121)); // Output: false
console.log(isPalindrome(10)); // Output: false
```
 **Time Complexity**:
- O(n), where n is the number of digits in `x`.    

 **Space Complexity**:
- O(n), as we create a new string and an array.