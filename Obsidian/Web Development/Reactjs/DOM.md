
ECMA scripts , ecma scripts standard --- js spec
loupe
settimeout was never part of ecma 
its a part of browser spec
settimeout , fetch ,setinterval, document -- browser spec
DOM ---- document 
class vs ids in html 
```html
<html>
  <script>
    function populateDiv() {
      // Retrieve values from input fields
      const a = document.getElementById("firstNumber").value;
      const b = document.getElementById("secondNumber").value;

      // Make a fetch API call to the backend
      fetch("<https://sum-server.100xdevs.com/sum?a=>" + a + "&b=" + b)
        .then(function(response) {
          // Parse the response as text
          response.text()
            .then(function(ans) {
              // Display the result in the "finalSum" div
              document.getElementById("finalSum").innerHTML = ans;
            });
        });
    }

			// Async function for populating the "finalSum" div
		    async function populateDiv2() {
		      // Retrieve values from input fields
		      const a = document.getElementById("firstNumber").value;
		      const b = document.getElementById("secondNumber").value;
		
		      // Make a fetch API call to the backend using async/await
		      const response = await fetch("https://sum-server.100xdevs.com/sum?a=" + a + "&b=" + b);
		      const ans = await response.text();
		
		      // Display the result in the "finalSum" div
		      document.getElementById("finalSum").innerHTML = ans;
		    }

  </script>
  <body>
    <!-- Input fields for numbers -->
    <input id="firstNumber" type="text" placeholder="First number"></input> <br></br>
    <input id="secondNumber" type="text" placeholder="Second number"></input> <br></br>

    <!-- Button to trigger the calculation -->
    <button onclick="populateDiv()">Calculate sum</button> <br></br>

    <!-- Display area for the final sum -->
    <div id="finalSum"></div>
  </body>
</html>
```
understanding why fetch call not working 

Debouncing 
```html
<html>
  <body>
    <!-- Input field with onInput event and debouncing -->
    <input id="textInput" type="text" onInput="debounce(handleInput, 500)" placeholder="Type something...">

    <!-- Display area for the debounced input value -->
    <p id="displayText"></p>

    <script>
      // Debounce function to delay the execution of a function
      function debounce(func, delay) {
        let timeoutId;

        return function() {
          // Clear the previous timeout
          clearTimeout(timeoutId);

          // Set a new timeout
          timeoutId = setTimeout(() => {
            func.apply(this, arguments);
          }, delay);
        };
      }

      // Function to handle the debounced onInput event
      function handleInput() {
        // Get the input field's value
        const inputValue = document.getElementById("textInput").value;

        // Display the input value in the paragraph
        document.getElementById("displayText").innerText = "You typed: " + inputValue;

        // Simulate sending a request (replace with actual AJAX call)
        console.log("Request sent:", inputValue);
      }
    </script>
  </body>
</html>
```

