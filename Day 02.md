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
