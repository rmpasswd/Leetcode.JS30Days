# Day 1 Hello World Task, Learning About Functions

Note from Leetcode Editorial, other docs…


## Different Ways to Function…

- **Basic function syntax:**
    
    ```js
    function fun(a, b) {
        const sum = a + b;
        return sum;
    }
    ```
    - Note that we cannot write `function fun(int a, int b){...}` because plain javascript do not support type declarations in *function parameters*. Typescript supports this syntax: `function fun(a: number, b: number){...}`

- **Anonymous Function:**
    
    ```jsx
    var f = function(a, b) { // We can omit function name *fun* and assign a variable
        const sum = a + b;
        return sum;
    }
    
    ```
    
- **Arrow Syntax:**
    
    ```js
    // 'function' keyword is omitted, and fun is the function's name
    var fun = (a,b) => { 
    	return a+b; // if there is only 1 line, can omit the return keyword and curly braces, see next codeblock..
    }
    console.log(fun(3, 4)); // 7
    ```
    
    ```js
    const addNprint = (i,j) => console.log(i+j);
    addNprint(4,5);

    // we can also omit the first parenthesis when there is only 1 parameter. fetch api example from freecodecamp:
    fetch('/json/cats.json')
	.then(response => response.json())
	.then(data => {
	document.getElementById('message').innerHTML = JSON.stringify(data);
	})
    ```

- **Immediately Invoked Function Expression (IIFE)** `( function description )(3,4 parameters);`
    
    ```js
    const result = (function(a, b) {
        const sum = a + b;
        return sum;
    })(3, 4); // this immediate parameter passing i.e. (3,4) makes the function invokable
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

## Higher Order Function => Functions within functions

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
console.log( createFunction()(2,5) ); // 7 //invoke in one line.

```

### Practical Use Case: Arity Check Mechanism

⇒ How to check if a function call has indeed been passed the expected number of parameters? without relying on error-exceptions.

Consider this simple greet function, just for demo purpose. We are calling the greet function from inside the object *someObj*.

```js
var someObj = {
    greetingText: greet
}
someObj.greetingText("Nat", "Willberg"); // this line is the function call

function greet(a,b){ // greet fun definition
    console.log("hello, ", a, b);
}
```

We Need to ensure that user passes 2 parameters, not 1, not 3.

```js
var someObj = {
    greetingText: argCheck(greet) // call another function argCheck with original greet function as parameter.
}

someObj.greetingText("Nat", "Willberg"); // this will not work now.
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
	
	    return fun.apply(self, arguments); // Run the Greet function if check passes. Use 'this' or 'null' instead of 'self' if faced error. ("In Node.js, self is not defined by default")
		}
}

// Reading: https://andrewberls.com/blog/post/javascript-tricks-enforcing-function-arity
```
### Practical Use Case: Memoization
**Reducing repetitive computation by storing the results, thus speeds up operations.**

For example, lets take a basic fibonacci series code:

```
function fibo( n) {
    if (n<2) return 1;
    return fibo(n-1) + fibo(n-2)
}
```
for n = 4 we will have to calculate fibo(3) and fib(2). 
fibo(3) will have to call fibo(2) and fibo(1). 
And fibo(2) will call fibo(1) and fibo(0).
Meaning we are calculating fibo(2) and many other twice.
We could store the result in a data structure(an object or a map) and just fetch the result instead of calculating the function again.

__fibbonacci with memoization__
```
// higher order function definition =>
function memoize(fun) {
	const cache = new Map(); // store immediate results in a map

  return function( ...args){
  	const key = JSON.stringify(args);

    if (!cache.has(key)){   // checks if we already have the result of higherOrderfunctionCall(100), otherwise calculates.
      cache.set(key, fun.apply(this, args)) 
      
    }
     return cache.get(key)
  }
}

function fibo( n) {
    if (n<2) return 1;

    return fibo(n-1) + fibo(n-2)  
}

const higherOrderfunctionCall = memoize(fibo)
higherOrderfunctionCall(100) // first time it will run slowly but then store the value to key '100'
higherOrderfunctionCall(100) // second time will be instant, it will use the 'cache'

```
- Note that if we replace line `return fibo(n-1) + fibo(n-2)` with the line `return memoize(fibo)(n-1) + memoize(fibo)(n-2)` ; we will not get faster speed, because `fibo(n-1)` and `fibo(n-2)` will run seperately. todo..

## Miscelleneous
### **return statement: comma vs plus + sign**
```js
function fun(value){
        return value, " or whatever"; // This will return a *tuple*.
}
console.log(fun(45)); // This will not return "45, or whatever".  console.log returns only the Last element of a *tuple*!
```
Instead always use + for string concatenation: ``` return value + "or whatev" ```



### More about arguments.length
    - returns an ‘array’ with limited array options. It is a keyword.
    - It only has length property, cannot insert delete elements
        - [https://2ality.com/2013/06/basic-javascript.html#sect_functions:~:text=Too many or too few arguments](https://2ality.com/2013/06/basic-javascript.html#sect_functions:~:text=Too%20many%20or%20too%20few%20arguments)
            
            ![image](https://github.com/rmpasswd/JS30Days/assets/35218856/ab4c52e7-3047-4894-93e0-4636b5be1a97)



- **More About Function Arguments: [The Spread syntax (...)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)**
    - Basic Use:
        
        ```js
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

    The followin function `log` takes a function definication as input and then returns a function which is basically a wrapper around the inputfunction with 2 console.logs
    ```jsx
    function log(inputpassFuntion) {
        return function(...args) {
            console.log("Input", args);
            const result = inputpassFuntion(...args);
            console.log("Output", result);
            return result;
        }
    }
    const f = log((a, b) => a + b); // this is calling log function and as a parameter passing an entire function implementation for adding 2 numbers.
    f(1, 2); // Input [1, 2] Output 3
    // another way is to first define our *inputpassFunction*
    function add(...args) {
    let arr = [...args]
    return arr.reduce( (accu, curr) => accu+=curr )
    }
    const f = log(add);
    f(5,1);
    // returns Input [5,1] Output 6
    ```
    

---

---

- Different runtime, unexplained.
    
    ![image](https://github.com/rmpasswd/JS30Days/assets/35218856/27cbad34-bcd7-4da1-a03f-8874600f228b)

	![image](https://github.com/rmpasswd/JS30Days/assets/35218856/bd568a5f-5c67-4026-9ae4-00b314f6d43f)
