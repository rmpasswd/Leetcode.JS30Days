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
If, before the delay of t milliseconds, the function cancelFn(in test code, not mine) is invoked, it should cancel the delayed execution of fn.  
Otherwise, if cancelFn is not invoked within the specified delay t, fn should be executed with the provided args as arguments.

If timeout t arrives then fn function will run with args, notice its an array of arguments thus the three dots.  
```js
var cancellable = function(fn, args, t) {
    var id = setTimeout( ()=> fn(...args),t)
    return () => clearTimeout(id)
};
```
### 2725.  Interval Cancellation  
This time we have to keep running the given function fn until we reach cancelTimeMs which is when cancel is invoked from the test code(not part of my submission).
Becase the cancelTimeMs argument is not my headache, I just need to keep running the fn function with setTimeout(wrong!) and provide a cancel function to call when required.

The function we have to use is setInterval and clearInterval. Leetcode's [editorial](https://leetcode.com/problems/interval-cancellation/solutions/3715176/interval-cancellation)  
```
var cancellable = function(fn, args, t) {
    fn(...args);

    let id = setInterval( ()=>{ fn(...args), t} ); // ***

    return = () => clearInterval(id)
     
};
```
Above code wont work. in the asterisk marked line, I did a strange typo thats also a programming feature called comma expression -_-  
For example: `a=(1,2,3)` this will evaluate to a=3  
C example:     `int sum = 0, result = (({for (int i = 0; i < 5; i++) sum += i;}), sum);`  
comma expression feature is that all the expression will evaluate from left to right. In the `result = (loop, sum)` part, first the left loop will evaluate and we will have a total sum, then the 'sum' after the comma will be assigned to result variable.  

In our js code, the two expressions `fn(..args)` and `t` are in a block seperated by comma, thus its a comma expression. Not serving our goal here though.

t should be the 2nd argument of setInterval, not fn. Easy fix, Done!  




