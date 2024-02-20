```js
var expect = function(val) {
    tobe: 20;
}

expecto1 = expect(10);

console.log(expecto1.tobe); // TypeError: Cannot read properties of undefined (reading 'tobe')
```

**Trying to access 'tobe' (as if it is a property) will not work because it is inside a function.**

Ways to access function properties with Dot notation .
Use an javascript object:
```js
var expect = {
    name: "To Be or Not to be",
    tobe: function(value){
        return (value + " or whatever");
    }
}
console.log(expect.tobe(4));
```

**or use a oop class:**
```js
class expect{
    constructor(value){
        this.value = value;
    }
    tobe(valueToCheck){
        if (this.value === valueToCheck) return {"value": true};
        else return {"error": false};
    }
}
exp1 = new expect(2);
console.log(exp1.tobe(3)); // this returns object as intended.
```


But we have to writing according to **Leetcode's boilerplate** inside a function =>
```js
    var expect = function(val) {
        // Write Logic here.
    };
 * expect(5).toBe(5); // true
 * expect(5).notToBe(5); // throws "Equal"
```

We can return an object and inside that object will be our 'property function' that returns true or throws equal/not equal,
```js
/**
 * @param {string} val
 * @return {Object}
 */
var expect = function(val) {
    return {
        toBe: function (valToCheck){
            if(val===valToCheck) return true;
            else throw "Not Equal"; // throw new Error("Not Equal");

            },

        notToBe: function (valToCheck){
            if(val!==valToCheck) return true;
            else throw "Equal";
        }
    }
};

/**
 * expect(5).toBe(5); // true
 * expect(5).notToBe(5); // throws "Equal"
 */
```
**More Robust**

```js
var expect = function(val) {
    return {
        toBe: (valToCheck) => {
            if(val!==valToCheck) throw "Not Equal";
            return true;    
            },

        notToBe: (valToCheck) => {
            if(val===valToCheck) throw "Equal";
            return true
        }
    }
};
```
