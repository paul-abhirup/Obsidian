https://leetcode.com/problems/reverse-integer/description/

```js

function reverse(x) {

    // handle negative numbers
    const isNegative = x < 0;  // checks if the number is negative 
    // If `x` is negative, we set a flag (`isNegative = true`) to remember that the result should also be negative.
    
    x = Math.abs(x);   // selects the absolute value of x

	// Operation
    let revNum = 0;
      while(x > 0){
      let  lastDigit = x % 10 ; //Extract the last digit
      revNum = (revNum * 10) + lastDigit ;

       x = Math.floor(x/10); // Remove the last digit of the num
      }

    // Handle overflow
    const maxInt = Math.pow(2,31) - 1; //2^31 -1
    const minInt = Math.pow(2,-31); // -2^31

	//Return 
     if (revNum > maxInt || revNum < minInt){
        return 0;
    } else {
        //Restore sign to the revNum and return
    return isNegative ? -revNum : revNum ;
    }    

};

```