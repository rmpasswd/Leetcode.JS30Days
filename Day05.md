2623. Memoize  
A memoized function is a function that will never be called twice with the same inputs. Instead it will return a cached value.  

```
function memoize(fn) {
    cache = new Map()    
     return function(...args) {
        if (cache.has(args)){ return cache.get(args)}
         r = fn.apply(this,args)
        cache.set(args,r)
        return r

    }
}
```
<img width="757" height="765" alt="image" src="https://github.com/user-attachments/assets/e35c3d60-a344-4532-a996-39274dce9625" />  

  
There is a subtle bug in above code.
```
const a = [1, 2];
const b = [1, 2];

console.log(a === b); // false ❗ (different objects)
```
So, when we use something like `Map.set(array,10) and Map.get(array)`, the array variable do not refer to the same array used in another earlier function call.  

Hence we have to stringify the array:  
```
function memoize(fn) {
    cache = new Map()    
     return function(...args) {
        key = JSON.stringify(args)
        if (cache.has(key)){ return cache.get(key)}
        r = fn.apply(this,args)
        cache.set(key,r)
        return r

    }
}
```
