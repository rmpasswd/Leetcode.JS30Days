```js
var expect = function(val) {
    tobe: 20;
}

expecto1 = expect(10);

console.log(expecto1.tobe); // TypeError: Cannot read properties of undefined (reading 'tobe')
```

**Trying to access 'tobe' as if it is a property will not work because it is inside a function.**

Ways to access function properties with Dot notation.:
```js
var expect = {
    name: "To Be or Not to be",
    tobe: function(value){
        return (value + " or whatever");
    }
}
console.log(expect.tobe(4));
```

**or use a class:**
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
