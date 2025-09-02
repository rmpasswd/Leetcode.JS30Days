
Everything to know about Promises from Lydia Hallie: https://medium.com/@lydiahallie/javascript-visualized-promises-async-await-a3f1aad8a943

Blunder:

The resolved value of a Promise is not supposed to directly accessible like `var v = Promise.result!` because that would stop the execution of the code, and it would not asynchronous and non-blocking like its supposed to be.

We can use _.then_ block to print out the value and use it inside the block:

```js
promise1 = new Promise(resolve => setTimeout(() => resolve(2), 20)), 
// // //

promise1.then( (value) => {
  console.log(value)
  PassToAnotherFun(value)
});  
```

Or, use async/await

```js
async function getval(){
  const v = await promise1
  return v
}
v = getval()
```

### 2723. Add Two Promises  
Given two promises promise1 and promise2, return a new promise. promise1 and promise2 will both resolve with a number. The returned promise should resolve with the sum of the two numbers.


```
var addTwoPromises = async function(promise1, promise2) {
        let v1 = await promise1;  
        let v2 = await promise2;
    let newpromise = new Promise( (res,rej) =>{
        // let v1 = await promise1; // error: await is only valid in async functions and the top level bodies of modules
        // let v2 = await promise2;
        res(v1+v2)
    } );
    return newpromise;
};
```
Issue: async function always returns a promise, no need to construct another new Promise. 

Solution:
```js
var addTwoPromises = async function(promise1, promise2) {
    return await promise1 + await promise2
};
```

