## Day 2


### Closures

A function can use variables that are *just outside* its scope!

> it has access to a reference to all the variables declared around it, also known as it's ***lexical environment.*** The combination of the function and its environment is called a ***closure***.
> 

```js
function createAdder(initial){
    function addi(b){
        return initial + b;
    }
    return addi;
}

const adder1 = createAdder(5);
const adder2 = createAdder(10); 
console.log(adder1(10)); // 15
console.log(adder2(10)); // 20
```

Example: Here each counter() holds the inner function only and because of closure can still access the value of "n". This is a feature of closure where **inner function still have access to outer function variable although outer function goes out of context after first call (createCounter(10)).**
```jsx
var createCounter = function (n) {
    
    return function () {
        return n++;
    };
};

/** 
 * const counterTen = createCounter(10)
 * counterTen() // 10
 * counterTen() // 11
 * counterTen() // 12
 */
 /** 
 * const counter20 = createCounter(10)
 * counter20() // 20
 * counter20() // 21
 * counter20() // 22
 */

```

### Similar Concept: Classes and Constructors

  ```js
  Class AdderClass{
    constructor(initial){  
      this.initialValue = initial;
  }
  add(b) {
    return this.initialValue + b;
    }
  }
const adderObj = new AdderClass( );
adderObj.add(10); //
  ```

- Differences:
> Besides differences in syntax, both code examples essentially serve the same purpose. They both allow you to pass in some state in a "constructor" and have "methods" that access this state.> 

> One key difference is that closures allow for true encapsulation. In the class example, there is nothing stopping you from writing addTo2.a = 3; and breaking it's expected behavior. However, in the closure example, it is theoretically impossible to access a. Note that as of 2022, true encapsulation is achievable in classes with # prefix syntax.> 

> Another difference is how the functions are stored in memory. If you create many instances of a class, each instance stores a single reference to the prototype object where all the methods are stored. Whereas for closures, all the "methods" are generated and a "copy" of each is stored in memory each time the outer function is called. For this reason, classes can be more efficient, particularly in the case where there are many methods.


```js
// Problem: Given an integer n, return a counter function. This counter function initially returns n and then returns 1 more than the previous value every subsequent time it is called (n, n + 1, n + 2, etc).

// Leetcode Solution =>

/**
 * @param {number} n
 * @return {Function} counter
 */
var createCounter = (n) => () => n++ ;

const counter = createCounter(10);

// calls.forEach( (eachcall, index) => counter(index));

/** 
 * const counter = createCounter(10)
 * counter() // 10
 * counter() // 11
 * counter() // 12
 */


    // vscode =>

//  var createCounter = function(n,i) {
    
//     return function(i) {
//         console.log(n+i);
//     };
// };

// const counter = createCounter(n);

// calls.forEach( (eachcall, index) => counter(index));
```
