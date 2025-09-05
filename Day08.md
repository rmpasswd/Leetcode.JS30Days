### 2637. Promise Time Limit
Given a time limitt and a function(which returns a Promise actually) to run within this time limit,,
We have let fn resolve if its within t or reject if t is exceeded.  

```
var timeLimit = function(fn, t) {
    
    return async function(...args) {
        return new Promise((res,rej)=>{
            // res(fn(...args)) 
            // Above is  wrong because we are calling res of the outer Promise, meaning the Promise has done its work, why should it go further down the line and process the reject inside setTimeout?!
            fn(...args).then(result=> res(result)).catch(rej) // But this works, becase we are waiting for fn to resolve (asynchronously). And following timeout line will also process, res or rej will win depending on the t value.
            setTimeout( ()=>{ rej("Time Limit Exceeded") },t )
        })
    }
};
```

