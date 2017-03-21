# Learning ECMAScript 6

## let

let you define variable in current scope only


## const

constant variable in current scope, not possible to modify in current scope; possible in different scope


## datatypes

``` javascript
document.write(typeof      true);    boolean
document.write(typeof      3.14);    number
document.write(typeof  "string");    string
document.write(typeof  Symbol());    symbol
document.write(typeof     {a:1});    object
document.write(typeof   [1,2,3]);    object
document.write(typeof undefined);    undefined
```


## string: template literal

aka string formatting, interpolation


## string: tag template literal

modify output using function


## string: as iterable

python style

``` javascript
string: method
string.repeat(3)
string.startsWith('s')
string.endsWith('s')
string.includes('ing')
```

##string: multiline

python style using backslash or backquote


##functions: default value

``` javascript

function getSum(a = 1, b = 1){
    document.write(`${a} + ${a} = ${a + b} <br />`)
}

function: rest parameters
function getSumMore(...vals){
    let sum = 0;
    for (let i = 0, len=vals.length; i < len; i++) {
        sum += vals[i]
    }
    document.write(`The sum is ${sum} <br />`);
}

getSumMore(1,2,3,4);

let vals = [1,2,3,4]
getSumMore(...vals);


function: arrow functions
let difference = (num1, num2) => num1 - num2;
document.write(`5 - 10 = ${difference(5, 10)} <br />`);

// can be multi-statement
let mult = (num1, num2) => {
    let product = num1 * num2;
    document.write(`${num1} * ${num2} = ${product} <br />`);
}

// functional style
let valArr = [1,2,3,4,5]

let sumVals = valArr.reduce((a,b) => a+b);
let evens   = valArr.filter(v => v % 2 == 0);
let doubles = valArr.map(v => 2 * v);
```

## objects: objects literal

``` javascript

function createAnimal(name, owner){
    return {
        name,
        owner,
        getInfo(){
            return `${this.name} is owned by ${this.owner}.`
        },
        address: {
            street: '123 Main St',
            city: 'Pittsburgh'
        }
    };
}

var spot = createAnimal("Spot", "Doug");
document.write(`${spot.name} is at ${spot.address.street}<br />`);

// introspection
Object.getOwnPropertyNames(spot)

//destructuring -- pattern matching like
let {name, owner} = spot;
let {address} = spot
document.write(`Street: ${address.street}<br />`);

// advance destructuring
favNums = [1, 2, 3]
let[,,chaos] = favNums  //chaos is now 3
let [, ...last2] = favNums  //last2 is 2

let a = 1, b = 2
[a, b] = [b, a]  // onplace switch
```


## class

``` javascript
class Mammal{
    constructor(name){
        this._name = name;
    }

    get name(){
        return this._name;
    }

    set name(name){
        this._name = name;
    }

    static makeMammal(name){
        return new Mammal(name);
    }

    getInfo(){
        return `${this.name} is a mammal`;
    }
}

let monkey = new Mammal("Fred");
monkey.name  //getter no need of _name
monkey.name = "Mark";

let chipmunk = Mammal.makeMammal( "Chipper");

class Marsupial extends Mammal{
    constructor(name, hasPouch){
        super(name);
        this._hasPouch = hasPouch;
    }

    get hasPouch(){
        return this._hasPouch
    }

    set hasPouch(hasPouch){
        this._hasPouch = hasPouch;
    }

    getInfo(){
        return `${this.name} is a marsuipal`;
    }
}

let kangaroo = new Marsupial("Paul", true);

//dynamic class inheritance
function getClass(classType){
    if(classType == 1){
        return Mammal;
    } else {
        return Marsupial;
    }

}

class Koala extends getClass(2){
    constructor(name){
        super(name);
    }
}
```


## symbols

like Elixir's atoms


``` javascript
let capital = Symbol("State capital");
let pennsylvania = {};
pennsylvania[capital] = "Harrisburg";

// sharing symbols
let employNum = Symbol.for("Employee Number");

let bobSmith = {}
bobSmith[employNum] = 10;

let sallyMark = {}
sallyMark[employNum] = 10;
```

## arrays

``` javascript

let array1 = Array.of(1,2,3);
let array2 = Array.from("hello world");
let array3 = Array.from(array1, (value) => value * 2);

for (let val of array3) document.write(`Array Val: ${val} <br />`);
```


## sets

``` javascript
var randSet = new Set();
randSet.add(10);
randSet.add("word");

randSet.has(10);  //true
randSet.size;  // 2
randSet.delete(10);

for (let val of randSet) document.write(`${val} <br \>`);
```


## maps

``` javascript
var randMap = new Map();
randMap.set("key1", "random string");
randMap.set("key1",  10);

randMap.get("key1");
randMap.get("key2");
randMap.size

randMap.forEach(function(value, key){
    document.write(`${key} : ${value} <br />`);
});
```


## promises

code to be executed later; either succeed or failed once; state = fullfill | rejected | pending | settle


``` javascript
// immediately handled promises
var p1 = Promise.resolve(" Resolve Me");
p1.then((res) => document.write(`${res}<br />`));

var p2 = new Promise(function(resolve, reject){
    setTimeout(() => resolve('Resolve Me again'), 2000)
});
p2.then((res) => document.write(`${res}<br />`));

//
let randVal = 18;
var p3 = new Promise(function(resolve, reject){
    if (randVal == 6){
        resolve("Good value.");
    } else {
        reject("Bad Value");
    }
});

p3.then(
    (val) => document.write(`${val}<br />`),
    (err) => document.write(`${err}<br />`)
);

// error handling
let randVal = 18;
var p4 = new Promise((resolve, reject) => {
    if (randVal <= 17){
        throw new Error("Can't vote.");
    } else {
        resolve("Can vote");
    }
});

p4.then((val) => document.write(`${val} <br />`))
  .catch((err) => document.write(`${err.message}`));

```
