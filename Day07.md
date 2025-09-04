### 2621. Sleep  

Given a positive integer millis, write an asynchronous function that sleeps for millis milliseconds. It can resolve any value.

We can assume, the solution will be checked by leetcode with this code. We have to define the sleep function here.
```
let t = Date.now();
sleep(100).then(() => {
  console.log(Date.now() - t); // 100
});
```

The boilerplate give is this: `async function sleep(millis) {}`

the docs say an async function always returns a promise,  
<img width="1447" height="332" alt="image" src="https://github.com/user-attachments/assets/26ba7289-a46b-42d2-bd45-6e0a169cc404" />  
Hence I thought to just use setTimeout and be done with it.  
```js
async function sleep(millis) {
    var r = setTimeout(()=>{
        return 123;
    }, millis) 

    return r;
}
```
But whats wrong with this code is that the return 123 line is inside a function(as the first argument of the settimeout. We cannot catch it! lets say millis is 3 seconds. and I have a console.log("hello") sitting above the return 123 line. I will see the console.log with no problem after 3 seconds. But I wont able to 'see' or catch the 123 value, unless I use Promise' resolve feature.    

  
<img width=45% height=45% alt="image" src="https://github.com/user-attachments/assets/db0a761d-cd48-49c0-ab6f-24a0f6bf2bf3" />  

=> setTimeout is just for execute code in its first argument after a delay, nothing more, nothing less.  Thus this below code will also not work!  

```js
async function sleep(millis) {
    return  setTimeout(()=> Promise.resolve(), millis);
}
```

Solution:  

```js
async function sleep(millis) {
    return new Promise(res => {
        setTimeout(()=> res(), millis)
    });
}
```




### 2715. Timeout Cancellation
If, before the delay of t milliseconds, the function cancelFn(in test code) is invoked, it should cancel the delayed execution of fn.  
Otherwise, if cancelFn is not invoked within the specified delay t, fn should be executed with the provided args as arguments.

If timeout t arrives then fn function will run with args, notice its an array of arguments thus the three dots.  
```js
var cancellable = function(fn, args, t) {
    var id = setTimeout( ()=> fn(...args),t)
    return () => clearTimeout(id)
};
```

