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
