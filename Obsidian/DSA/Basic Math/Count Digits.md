https://www.geeksforgeeks.org/problems/count-digits5716/1

```js


// User function Template for javascript

/**
 * @param {number} n
 * @returns {number}
 */

class Solution {
    // Function to check how many digits of n evenly divide n.
     evenlyDivides(n) {
        //  code here
        let count = 0;
        const originalN = n; // Store the original value of n

        while (n > 0) {
            const digit = n % 10; // Extract the last digit
            if (digit !== 0 && originalN % digit === 0) { // Check if the digit divides n evenly
                count++;
            }
            n = Math.floor(n / 10); // Remove the last digit
        }

        return count;
    }
}

// // Example usage:
// const solution = new Solution();
// console.log(solution.evenlyDivides(12));    // Output: 2
// console.log(solution.evenlyDivides(2446)); // Output: 1
// console.log(solution.evenlyDivides(23));   // Output: 0




// using Function based example

function countDigitsThatDivide(n) {
    let count = 0;
    const originalN = n; // Store the original value of n

    while (n > 0) {
        const digit = n % 10; // Extract the last digit
        if (digit !== 0 && originalN % digit === 0) { // Check if the digit divides n evenly
            count++;
        }
        n = Math.floor(n / 10); // Remove the last digit
    }

    return count;
}

```