2703. Return Length of Arguments Passed  
This is one line solution.
```js
var argslengthfun = function(...args){
  return args.length // uses the args variable
  return argument.length  // uses the 'argument' keyword, available for every non-arrow function in javascript2703. Return Length of Arguments Passed
  
```
<img width="1298" height="128" alt="image" src="https://github.com/user-attachments/assets/3726bac0-340c-452d-9ed7-51aeda53ec8b" />

Notice that a function below with 3 parameters.
```
function func1(a, b, c) {
  console.log(arguments.length);
}
```
This does not mean `arguments.length` will always return 3.  `func1(11,22)` will return 2.  
Meaning argments.length returns exactly the number of arguments *passed*, regardless of the three parameters in function definition.

2666. Allow One Function Call
In many cases, the user can invoke the function more than once, but we want it to evaluate only the first time and ignore the other calls. Use Cases: 
- API Calls – Fetch data only once, even if the fetch function is called multiple times.
- Event Listeners– Attach an event handler to an element once to avoid multiple triggers.
- Singletons– Create a single instance of an object or resource.
```js
//    let called = false // putting this line here fails test cases.
var once = function(fn) {
    let called = false // this works.
    return function(...args){
        if (!called) {
            called = true
            return fn.apply(this,args)
        }
        return undefined
    }
};
```
A closure is simply:
"A function that remembers variables from its outer scope, even after that outer function has finished running".

