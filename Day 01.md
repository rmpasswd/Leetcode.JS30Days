# Day 1 Hello World Task, Learning About Functions

Note from Leetcode Editorial, other docs…

### Different Ways to Function…

- **Basic function syntax:**
    
    ```sql
    function fun(a, b) {
        const sum = a + b;
        return sum;
    }
    ```
    

- **Anonymous Function:**
    
    ```jsx
    var f = function(a, b) { // We can omit function name *fun* and assign a variable
        const sum = a + b;
        return sum;
    }
    
    ```
    
- **Arrow Syntax:**
    
    ```sql
    // 'function' keyword is omitted, and fun is the function's name
    var fun = (a,b) => { 
    	return a+b; // if there is only 1 line, can omit the return keyword and curly braces, see next codeblock..
    }
    console.log(fun(3, 4)); // 7
    ```
    
    ```sql
    const addNprint = (i,j) => console.log(i+j);
    
    addNprint(4,5);
    ```
    
- **Immediately Invoked Function Expression (IIFE)** `( function description )(3,4 parameters);`
    
    ```sql
    const result = (function(a, b) {
        const sum = a + b;
        return sum;
    })(3, 4);
    console.log(result); // 7
    ```
    
    - Leetcode editorial:
        
        > Why would you write code like this? It gives you the opportunity to ***encapsulate*** a variable within a new ***scope***. For example, another developer can immediately see that `sum` can't be used anywhere outside the function body.
        > 
        
        > **Differences between arrow syntax and function syntax**.
        > 
        > 1. More minimalistic syntax. This is especially true for anonymous functions and single-line functions. For this reason, this way is generally preferred when passing short anonymous functions to other functions.
        > 2. No automatic hoisting. You are only allowed to use the function after it was declared. This is generally considered a good thing for readability.
        > 3. Can't be bound to `this`, `super`, and `arguments` or be used as a constructor. These are all complex topics in themselves, but the basic takeaway should be that arrow functions are simpler in their feature set. You can read more about these differences [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions).
        > 
        > The choice of arrow syntax versus function syntax is primarily down to preference and your project's stylistic standards.
        > 

---

**Functions within functions ⇒**

```jsx
function createFunction() {
    function f(a, b) {
        const sum = a + b;
        return sum;
    }
    return f;
}
const fun = createFunction();
console.log(fun(3, 4)); // 7
```

### In the Wild: Arity Check Mechanism

⇒ How to check if a function call has indeed been passed the expected number of parameters? not relying on error-exceptions.

Consider this simple greet function, just for demo purpose. We are calling the greet function from inside the object *someObj*.

```sql
var someObj = {
    greetingText: greet
}
someObj.greetingText("Nat", "Willberg");

function greet(a,b){
    console.log("hello, ", a, b);
}
```

What if we Need to ensure that user passes 2 parameters, not 1, not 3.

```sql
var someObj = {
    greetingText: argCheck(greet) // call another function argCheck with original greet as parameter.
}

someObj.greetingText("Nat", "Willberg"); // this will not work, greetingText is not a function. 
// someObj.greetingText = ["Nat", "Willberg"]; this works!

function greet(a,b){
    console.log("hello, ", a, b);
}

// argCheck checks whether number of parameters passed to it equals to the number of parameters its function argument(fun = greet) can take.
// Note that js is flexible in the number of parameters we can pass to a function.
function argCheck(fun){
		return function() {  // return ()=> {
	    if (arguments.length !=fun.length ){
	        console.log("Mismatch number of arguments, Got ", arguments.length, " But expected ", fun.length);
	        return;
	    }
	
	    return fun.apply(self, arguments); // Run the Greet function if ok.
		}
}

// Reading: https://andrewberls.com/blog/post/javascript-tricks-enforcing-function-arity
```

- More about arguments ‘array’. It is a keyword.
    - It only has length property, cannot insert delete elements
        - [https://2ality.com/2013/06/basic-javascript.html#sect_functions:~:text=Too many or too few arguments](https://2ality.com/2013/06/basic-javascript.html#sect_functions:~:text=Too%20many%20or%20too%20few%20arguments)
            
            ![image](https://github.com/rmpasswd/JS30Days/assets/35218856/ab4c52e7-3047-4894-93e0-4636b5be1a97)



- **More About Function Arguments: [The Spread syntax (...)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)**
    - Basic Use:
        
        ```sql
        function sum(x, y, z) {
          return x + y + z;
        }
        
        const numbers = [1, 2, 3];
        
        console.log(sum(...numbers));
        ```
        
    - 
    
    > mdn docs:
    > 
    > 
    > Spread syntax can be used when all elements from an object or array need to be included in a new array or object, or should be applied one-by-one in a function call's arguments list. There are three distinct places that accept the spread syntax:
    > 
    > - [Function arguments](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax#spread_in_function_calls) list (`myFunction(a, ...iterableObj, b)`)
    > - [Array literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax#spread_in_array_literals) (`[1, ...iterableObj, '4', 'five', 6]`)
    > - [Object literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax#spread_in_object_literals) (`{ ...obj, key: 'value' }`)
    
    ```jsx
    function log(inputFunction) {
        return function(...args) {
            console.log("Input", args);
            const result = inputFunction(...args);
            console.log("Output", result);
            return result;
        }
    }
    const f = log((a, b) => a + b);
    f(1, 2); // Logs: Input [1, 2] Output 3
    ```
    

---

---

- Different runtime, unexplained.
    
    ![image](https://github.com/rmpasswd/JS30Days/assets/35218856/27cbad34-bcd7-4da1-a03f-8874600f228b)

	![image](https://github.com/rmpasswd/JS30Days/assets/35218856/bd568a5f-5c67-4026-9ae4-00b314f6d43f)
