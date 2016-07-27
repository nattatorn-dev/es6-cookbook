# React-Redux-ES6-Cookbook
Recipes for making your React.js Components Awesome

# Table of Contents
1. [Functional](#functional-intro)
2. [Let, Const](#let-const)
3. [Arrow Function](#arrow-function)
4. [Template Strings](#template-strings)
5. [Classes](#classes)
6. [Spread Operator](#spread-operator)
7. [Union, Intersection, Difference](#union-intersection-difference)
8. [Map](#map)
9. [Array](#array)
10. [Promise](#promise)
11. [Default, Rest, Spread](#default-rest-spread)
12. [Destructuring](#destructuring)
13. [Iterator](#iterator)
14. [Others](#others)
15. [Labs](#labs) 
16.[Math] (#math)
17. [Map, Set, WeakMap, WeakSet] (#map-set-weakMap-weakSet)
18. [Redux] (#redux)
19. [Tips] (#tips)
20. [Algorithm] (#algorithm)


#### functional intro
### Recursion
```js
// normal
var counter = 10;
while(counter > 0) {
    console.log(counter--);
}

// Tail call optimization
const countdown = (counter) => {
  if(counter > 0) {
    console.log(counter)
    return countdown(counter - 1)
  } return counter
}
countdown(10) //10~0
```
### Compose
```js
const convertSpaceToDash = (text) => { return text.replace(' ', '-') }
const lowercase = (text) => { return text.toLowerCase() }
const prefix = (text) => { return `# ${text}` }

// fix args es5
const composeTree = (f1, f2) => {
  return (res1) => {
    return f1(f2(res1))
  }
}

const convertSpaceToDashLowercase = composeSpread(
  convertSpaceToDash, 
  lowercase
)

console.log(convertSpaceToDashLowercase('Hello World')) // hello-world

// compose spread you can pass multi param to compose function
let composeSpread = (...fns) => fns.reduce((f, g) => (...args) => f(g(...args)));

const convertSpaceToDashLowercaseAndPredfix = composeSpread(
  convertSpaceToDash, 
  lowercase,
  prefix
)

console.log(convertSpaceToDashLowercaseAndPredfix('Hello World')) // # hello-world
```
#### Let, Const
### Const
```javascript
const names = ['Jordan', 'mark']
names.push('bella')
console.log( names ) //['Jordan', 'mark', bella]

const names = {name: 'mark'}
names.age = 12
console.log( names ) // Object {name: "mark", age: 12}
// Here’s a simple example. In the code below we create a new variable with a constant reference to an Array. We can then add values onto the array and since this does not change the reference, everything works

	
const names = [];
names = [];  // Error!
// Of course, if you have a const that points to a primitive such as a string or number, then there really isn’t anything to change about that value. All methods on String and Number return new values (objects)
primitive type
- Number
- String
- Booleanl
- undefined
- null

reference type 
- Object
- Array
- Function
- Date
- RegExp
```
### Var, Let
```javascript

var users = 100
var users = 25
console.log(users) // 25

let users = 100
let users = 25
console.log(users) // err

var number = 0

{
  let number = 2
  console.log(number)
}

console.log(number)
// 0
// 2

var number = 0

{
  var number = 2
  console.log(number)
}

console.log(number)
// 2
// 2

```

#### declare let outter scope and innner scope
```javascript 

//real world
let users = ['mark','john', 'sara']

{
  let users = ['jenny']
  console.log(users) // ["jenny"]
}
console.log(users) // ['mark','john', 'sara']
  

let users = ['mark','john', 'sara']

{
  console.log(users) // undefined
  
  let users = ['jenny']
  console.log(users) // ["jenny"]
}

var users = ['mark','john', 'sara']

{
  console.log(users) // ["mark", "john", "sara"]

  var users = ['jenny']
  console.log(users) // ["jenny"]
}
```
#### Arrow Function
![Arrow Function](http://www.uxebu.com/wp-content/uploads/2015/05/arrow-function4-150px-150x134.jpg)
##### exmaple 1
```javascript
let arr = [1, 2, 3]
// es5
arr.map(function(val) { return val * 2 }) // [2, 4, 6]

// es6
arr.map(val => val * 2) // [2, 4, 6]


const isThree = num => num === 3;
const containsThree = arr => !!arr.find(item => item === 3);

// es5
var func = function (param) {
    return param.split(" ");
}

// es6
let func = param => param.split(" ");

func("Felipe Moura"); // returns ["Felipe", "Moura"]

```
##### exmaple 2
```javascript
let a = [
  "Hydrogen",
  "Helium",
  "Lithium",
  "Beryl­lium"
];

let a2 = a.map(function(s){ return s.length });

let a3 = a.map( s => s.length );
```
##### exmaple 3
```javascript
// normal
function(arg) {
  // do something
}

// Use arrow function
(arg) => {
  // do something
}

// share the same this as surrounding code.
let bob = {
  _name: "Bob",
  _friends: [],
  printFriends() {
    this._friends.forEach(function(friend) {
      console.log(this._name + " knows " + friend);
    });
  },
  printFriendsWithArrowFunction() {
    this._friends.forEach((friend) => {
      console.log(this._name + " knows " + friend);
    });
  }
};

bob._friends.push('Tae');

bob.printFriends(); // Cannot read property '_name' of undefined
bob.printFriendsWithArrowFunction(); // "Bob knows Tae"
```
##### exmaple 4: Immediately-invoked
```javascript
( x => x * 2 )( 3 ); // 6

( (x, y) => {
    x = x * 2;
    return x + y;
})( 3, "A" ); // "6A"
```

#### Template strings
##### example 1
```javascript
// operator
let number1 = 10,
    number2 = 22;

let sum = `${number1} + ${number2} = ${number1 + number2}`

console.log(sum); // 10 + 22 = 32

// multi-line syntax
let myFav = `javascript
sass
c#
ruby`

console.log(myFav) // javascript
                   // sass
                   // c#
                   // ruby
```
##### exmaple 2
```javascript
// define and using a template
const tmpl = addrs => html`
      <table>
      ${addrs.map(addr => html`
          <tr>$${addr.first}</tr>
          <tr>$${addr.last}</tr>
      `)}
      </table>
  `;

// the template is used like this
console.log(tmpl([
  { first: '<Jane>', last: 'Bond' },
  { first: 'Lars', last: '<Croft>' },
]));

// output
<table>

      <tr>Jane</tr> 
      <tr>&lt;Bond&gt;</tr>

      <tr>&lt;Lars&gt;</tr>
      <tr>Croft</tr>

</table>
```
#### Classesa
##### exmaple 1
```javascript
class SkinnedMesh extends THREE.Mesh {
  constructor(geometry, materials) {
    super(geometry, materials);

    this.idMatrix = SkinnedMesh.defaultMatrix();
    this.bones = [];
    this.boneMatrices = [];
    //...
  }
  update(camera) {
    //...
    super.update();
  }
  get boneCount() {
    return this.bones.length;
  }
  set matrixType(matrixType) {
    this.idMatrix = SkinnedMesh[matrixType]();
  }
  static defaultMatrix() {
    return new THREE.Matrix4();
  }
}
```
##### exmaple 2
```javascript
class Constroctor {
  constructor(height, weight, bedroom, bathroom, people, address, rental) {
    this.height = height
    this.weight = weight
    this.bedroom = bedroom
    this.bathroom = bathroom
    this.people = people
    this.address = address
    this.rental = rental
  }
  
  getArea() {
    return this.height * this.weight
  }
  
  getRental() {
    return this.rental
  }
  
  getTotalRoom() {
    return this.bedroom + this.bathroom
  }
  
  getInformation() {
    return `Total room: ${this.getTotalRoom()} (${this.bedroom} bedroom ${this.bathroom} bathroom)
Area: ${this.address}`
  }
}

class Condo extends Constroctor {
  constructor(height, weight, bedroom, bathroom, people, address, rental, nearestStation, commonFeeCharge){
    super(height, weight, bedroom, bathroom, people, address, rental)
    this.nearestStation = nearestStation
    this.commonFeeCharge = commonFeeCharge
  }
  
  getInformation() {
    return `Total: ${super.getArea()} sq. 
Pricing: ${super.getRental()} month
${super.getInformation()}
Nearest Station: ${this.nearestStation}
Common fee charge: ${this.commonFeeCharge} month`
  }
}

let siri = new Condo(40, 120, 2, 1, 1, 'Huai Khwang', 6500, 'MRT Huai Khwang', 1500)
console.log(siri.getInformation())


//output
Total: 4800 sq. 
Pricing: 6500 month
Total room: 3 (2 bedroom 1 bathroom)
Area: Huai Khwang
Nearest Station: MRT Huai Khwang
Common fee charge: 1500 month
```
##### import-export
```javascript
//lib.js
export const a = 2;
export function b(x) {
    return x * x;
}

//
import { a, b } from 'lib';
console.log(a) // 2
console.log(b(a)) // 4

//
import * as lib from 'lib';
console.log(lib.a) // 2
console.log(lib.b(a)) // 4

//
export default function () { ... };
import myFunc from 'myFunc';

myFunc();

export default class { ... };
import MyClass from 'MyClass';

let inst = new MyClass();
```
#### Spread Operator
```javascript
// example 1
let params = [ "hello", true, 7 ]
let other = [ 1, 2, params ] // [ 1, 2, "hello", true, 7 ]
f(1, 2, params) === 9

let str = "foo"
let chars = [str] // [ "f", "o", "o" ]

// example 2
let items1 = [1,2,3,4]
let items2 = [5,6,7,8]

function spreadForeach1 (...items) {
  items.forEach(function (item) {
      console.log(item)
  })
}

spreadForeach1(items1,items2) 
// [1,2,3,4]
// [5,6,7,8]

function spreadForeach2 (...items) {
  items.forEach(function (item) {
      console.log(item)
  })
}

spreadForeach2(...items1)
// 1
// 2
// 3
// 4
```
#### Spread Operator II
```javascript
// es5
function max() {  
  // arguments contains all params, named + non-named
  // we use Function#apply to pass those as individual arguments
  return Math.max.apply(null, arguments);
}
// => 18

// es6
const max = (...nums) => Math.max(...nums)
max(5,18,1,8)
// => 18

// es5
function join(sep /*, ...args*/) {  
  var args = [].slice.call(arguments, 1)
  return args.join(sep)
}

// => one:two:three
// es6
const join = (sep, ...args) => args.join(sep)
join(':', "one", "two", "three")
//=> one:two:three

// es5
let merged = Object.assign(base, src1, src2);
// => { a: 1, b: 3, c: 4 }

// es6
merged = {  
    ...base,
    ...src1,
    ...src2
  };
// => { a: 1, b: 3, c: 4 }
```
#### Union, Intersection, Difference
```javascript
// union
let a = new Set([1, 2, 3]);
let b = new Set([4, 3, 2]);
let union = new Set([...a, ...b]);
// {1,2,3,4}

// intersection
let a = new Set([1, 2, 3]);
let b = new Set([4, 3, 2]);
let intersection = new Set(
[...a].filter(x => b.has(x)));
// {2,3}

// difference
let a = new Set([1, 2, 3]);
let b = new Set([4, 3, 2]);
let difference = new Set(
[...a].filter(x => !b.has(x)));
// {1}

[credit: Dr. Axel Rauschmayer](http://www.2ality.com/2015/01/es6-set-operations.html)
```
#### Map
##### Exmaple 1 (Basic operations, size, clear and chainable)
```javascript
let map = new Map();
map.set('dog', 123);
map.get('dog')
// 123

map.has('dog')
// true

map.delete('dog')
// true

map.has('dog')
false

let map = new Map();
map.set('dog', true);
map.set('cat', false);

map.size
// 2
map.clear();
map.size
// 0

let map = new Map([
    [ 1, 'dog' ],
    [ 2, 'cat' ],
    [ 3, 'fish' ]
]);

// the set method is chainable
let map = new Map()
.set(1, 'dog')
.set(2, 'cat')
.set(3, 'fish');
```
#### Array
##### reduce
```js
[0, 1, 2, 3, 4].reduce( (prev, curr) => prev + curr ) // 10


let flattened = [[0, 1], [2, 3], [4, 5]].reduce((prev, curr) => {
   prev.concat(curr)
}, [])

console.log(flattened) // [0, 1, 2, 3, 4, 5]

let developers = [
    { name: 'Joe', age: 23, gender: 'male' },
    { name: 'Sue', age: 28, gender: 'male'  },
    { name: 'Jon', age: 32, gender: 'female'  },
    { name: 'Bob', age: 24, gender: 'male'  }
]


let totalAge = developers.reduce((prev, curr) => {
     prev + curr.age;
}, 0);

console.log(totalAge) // 107


let selectByGender = developers.reduce((prev, curr, index) => {
  prev[curr.gender].push(curr)
  return total
}, {female: [], male: []})

console.log(selectByGender)

// {
//     "female": [{
//         "name": "Jon",
//         "age": 32,
//         "gender": "female"
//     }],
//     "male": [{
//         "name": "Joe",
//         "age": 23,
//         "gender": "male"
//     }, {
//         "name": "Sue",
//         "age": 28,
//         "gender": "male"
//     }, {
//         "name": "Bob",
//         "age": 24,
//         "gender": "male"
//     }]
// }

let array = [[1, 2], [3, 4], [5, 6]].reduce((prev, curr, index) => {
  return prev.concat(curr)
},[])

console.log(array) //[1, 2, 3, 4, 5, 6]



let developerList = developers.reduce((prev, curr, index) => {
  prev.push(curr.name)
  return prev
},[])


console.log(developerList.join(', ')) // Joe, Sue, Jon, Bob



// example - 1
var numbers = [1, 2, 3, 4]
var newNumbers = []

for(var i = 0; i < numbers.length; i++) {
    var number = numbers[i]
    newNumbers.push(number)

    if(number % 2 === 0) {
        newNumbers.push(number)
    }
}

console.log("The final numbers are", newNumbers); // [1, 2, 2, 3, 4, 4]

// example - 2
let numbers = [1, 2, 3, 4];
let newNumbers = numbers.reduce((newArray, number) => {
    newArray.push(number);

    if(number % 2 === 0) {
        newArray.push(number)
    }
    return newArray
}, [])

console.log("The final numbers are", newNumbers); // [1, 2, 2, 3, 4, 4]


// example
[
    { doctorNumber: "#9",  playedBy: "Christopher Eccleston", yearsPlayed: 1 },
    { doctorNumber: "#10", playedBy: "David Tennant",         yearsPlayed: 6 },
    { doctorNumber: "#11", playedBy: "Matt Smith",            yearsPlayed: 4 },
    { doctorNumber: "#12", playedBy: "Peter Capaldi",         yearsPlayed: 1 }
] 

// example - 1
doctors = doctors.filter(function(doctor) {
    return doctor.begin > 2000; // if truthy then keep item
}).map(function(doctor) {
    return { // return what new object will look like
        doctorNumber: "#" + doctor.number,
        playedBy: doctor.actor,
        yearsPlayed: doctor.end - doctor.begin + 1
    };
});

console.log(JSON.stringify(doctors, null, 4));


// example - 2
doctors = doctors.reduce(function(memo, doctor) {
    if (doctor.begin > 2000) { // this serves as our `filter`
        memo.push({ // this serves as our `map`
            doctorNumber: "#" + doctor.number,
            playedBy: doctor.actor,
            yearsPlayed: doctor.end - doctor.begin + 1
        });
    }
    return memo;
}, []);

console.log(JSON.stringify(doctors, null, 4));


// http://cryto.net/~joepie91/blog/2015/05/04/functional-programming-in-javascript-map-filter-reduce/
// http://elijahmanor.com/reducing-filter-and-map-down-to-reduce/
```
#### Promise
##### Example 1
```javascript

// old pattern
$.ajax('/stuff', {
  success: function(){
    console.log('succeeded');
  },
  error: function(){
    console.log('failed');
  }
});

// es6
fetch('/stuff')
  .then(function(){
    console.log('succeeded')
  })
  .catch(function(){
    console.log('failed')
  });

// multi task
$.ajax('./stuff', {
    success: function(){
      $.ajax('./todo_stuff',{
        success: function(){
          console.log('call todo_stuff is succeeded');
        },
        error: function(){
          console.log('error')
        }
      });
    },
    error: function(){
      console.log('error');
    }
});

// es6
fetch('/stuff')
  .then(function(){
     return fetch('/todo_stuff');
  })
  .then(function(){
      console.log('call todo_stuff in succeeded');
  })
  .catch(function(){
      console.log('error');
  });
```
##### Example 2
```javascript
let promise = new Promise((resolve, reject) => {

  // when success, resolve  
  let value = 'success';
  resolve(value);

  // when an error occurred, reject
  reject(new Error('Something happened!'));
});
promise.then(response => {
  console.log(response);
}, error => {
  console.log(error);
});

// success
```
##### Example 3
```javascript
function a () {
  return new Promise((resolve, reject) => {
    let value = true
    if(value) {
      resolve('success')
    }
    else {
      reject('err')
    }
  })
}

function b () {
  return new Promise((resolve, reject) => {
    let value = true
    if(value) {
      resolve('success')
    }
    else {
      reject('err')
    }
  })
}

function c () {
  return new Promise((resolve, reject) => {
    let value = true
    if(value) {
      resolve('success')
    }
    else {
      reject('err')
    }
  })
}

function testPromise () {
  a()
  .then((data) => {
    console.log(`a ${data}`)
    return b()
  })
  .then((data)=>{
    console.log(`b ${data}`)
    return c()
  })
  .then((data) => {
    console.log(`c ${data}`)
  })
  .catch((err) => {
    console.log(err)
  })
  
}

testPromise()
// a success
// b success
// c success
```

#### Default, Rest, Spread
```javascript
// default
let divided = function(number, divisor = 2){
    return number / divisor;
}

console.log(divided(4, 2)); // 2
console.log(divided(2));    // 1
console.log(divided(2, undefined));    // 1
console.log(divided(2, null));    // 1

// rest: example 1
function size(...theArgs) {
  console.log(theArgs.length);
}

size(1, 2, 4, 6,{'number': 1 },[1, 2, 3]); // 6

// example 2
function sum(...numbers) {
  let result = 0;

  numbers.forEach(function (number) {
    result += number;
  });
  return result;
}

console.log(sum(2)); // 2
console.log(sum(2, 4, 6)); // 12

// spread: example 1
function sum(a, b, c) {
  return a + b + c;
}

let args = [1, 2, 3];

console.log(sum.apply(undefined, args)); // 6


let evenNumbers = [2, 4], oddNumbers = [1, 3]

console.log(sum.apply(...evenNumbers, ...oddNumbers, 100))

// example 2
function minus(a, b){
	return a - b;
}

let evenNumbers = [2, 4, 6], oddNumbers = [1, 5]

console.log(minus(...evenNumbers)) // -2
console.log(minus(...oddNumbers)) // -4
```

#### Destructuring
```javascript
let user = {
  id: 1,
  name: {
    firstname: 'john',
    lastname: 'henly'
  },
  age: 25,
  email: 'abc@todo.com',
  friends: [
    'mark', 'mila', 'luna'
  ],
  socials: [
    'abc@fackbook', 'abc@google', 'abc@github'
  ]
}
// es5
console.log(user.name.firstname); // john

// destructuring with es6
let { id: user_id,
     	name: {firstname: user_firstname, lastname: user_lastname},
     	age: user_age,
     	email: user_email,
      friends: [friend1, , friend3],
    	username: user_username} = user // can also be used user()

console.log(user_age, user_email); // 25 'abc@todo.com'
console.log(friend3); // luna
console.log(user_username); // undefined
```

#### Iterator
```javascript
// for-of loop
for (LET of ITERABLE) {
  CODE BLOCK
}

// Arrays in ES6 are iterable by default, we can even use a break, continue and return.
const arr = [1, 2, 3, 4, 5];
for (let item of arr) {
  if (item > 4) {
    break;
  }
  if (0 !== item % 2) {
    continue;
  }
  console.log(item); // 2
                     // 4
}
```

#### redux

```javascript
return Object.assign({}, state, {
 visibilityFilter: action.filter
})
return { ...state, visibilityFilter: action.filter }
 
 
return getAddedIds(state.cart).map(id => Object.assign(
 {},
 getProduct(state.products, id),
 {
 quantity: getQuantity(state.cart, id)
 }
))

return getAddedIds(state.cart).map(id => ({
 ...getProduct(state.products, id),
 quantity: getQuantity(state.cart, id)
}))
```

#### Other
```javascript
// Computed Property Names
// es5
var prefix = 'users_';
var myObject = {};

myObject[prefix + 'name'] = 'nattatorn';
myObject[prefix + 'age'] = 25;

console.log(myObject['users_name']); // nattatorn
console.log(myObject['users_age']); // 25

// es6
var prefix = 'users_';
var myObject = {
  [prefix + 'name']: 'nattatorn',
  [prefix + 'age']: 25
};

console.log(myObject['users_name']); // nattatorn
console.log(myObject['users_age']); // 25
```
```javascript
// Obj Initializer Shorthand
function getPoint() {
  var x = 1;
  var y = 10;

  return {x, y};
}

getPoint(); // { x: 1, y: 10 }
```
##### Labs
```javascript
// es6
let emp = {
	firstname: 'nattatorn',
  lastname: null,
  age: 25,
  friends: ['mike', 'aof', 'earth', 'big'],
  emails: ['nat@gmail.com', 'nat-work@gmail.com', 'nat@facebook.com'],
  github: ['nat@github.com', 'nat-test@github.com'],
  bitbucket: ['nat@bitbucket.com']
}

let {friends: _myFriends, emails: _myEmails, github: _git_emails, bitbucket: _bitbucket_emails } = emp;

function sayHello({firstname: myFirstName, lastname: myLastName}){
	return `hello! ${myFirstName || '(No first name)'} ${myLastName || '(No last name)'}, I'm glad to see you again.`
}

function knowFrineds(myFriends){
  return render = myFriends.map(v => `
i know ${v}.`);
}

function haveEmails(...myEmails){
  let type_emails = [], emails = [];
	for(type of myEmails){

      type.map((v, i) => {
      	if(i === 0){
          v = `firstitem: ${v}`;
        }
        emails.push(v);
    	}
		)
  }
  return {type_emails, emails}
}

console.log(sayHello(emp)); // hello! nattatorn (No last name), I'm glad to see you again.
console.log(knowFrineds(_myFriends)); // ["↵i know mike.", "↵i know aof.", "↵i know earth.", "↵i know big."]
console.log(haveEmails(_myEmails, _git_emails, _bitbucket_emails));
```
##### Math
```javascript
let choicesKey = ['a', 'b', 'c', 'd'];
let max = 9;

function* random (max) {
   yield Math.floor(Math.random() * max) + 1;
}

function singleRandom (max) {
   return Math.floor(Math.random() * max) + 1;
}

function* randomMath () {
   while (true) {
     yield* random(max);
   }
}

function* randomOperator () {
  while (true) {
     yield operators[Math.floor(Math.random() * operators.length)];
  }
}
let answer = Math.floor(eval(variableB + operatorA + variableA)); // 5 + 5 = _ ?
let ques = `${variableA} ${operatorA} ${variableB} = _ ?` // 10

```
##### Labs random, remove, range
```javascript
// shuffle
function shuffle(array) {
 let counter = array.length;

  while (counter > 0) {
    let index = Math.floor(Math.random() * counter);
     counter--;
    let temp = array[counter];
     array[counter] = array[index];
     array[index] = temp;
  }
  return array;
}

let numbers = [1, 2, 3, 4]; // [1, 2, 3, 4]
let transform = shuffle(numbers); // [2, 4, 1, 3]

// randomAndPickOne
function randomAndPickOne(arrays) {
  return arrays[Math.floor(Math.random() * arrays.length)];
}

let numbers = [1, 2, 3, 4]; // [1, 2, 3, 4]
let transform = randomAndPickOne(numbers); // 2

// removeValueOfArrays
function removeValueOfArrays(arr) {
  var what, a = arguments,
    L = a.length,
    ax;
  while (L > 1 && arr.length) {
    what = a[--L];
    while ((ax = arr.indexOf(what)) !== -1) {
      arr.splice(ax, 1);
    }
  }
  return arr;
}

let strings = ['cat', 'dog']; // ['cat', 'dog']
let transform = removeValueOfArrays(strings, 'cat'); // ['dog']

// range
function rangeString(first, last) {
  var a = first.charCodeAt(0)
  var b = last.charCodeAt(0) + 1
  return Array.apply(null, {
      length: Math.abs(b - a)
    })
    .map(function(x, i) {
      return String.fromCharCode(Math.min(a, b) + i)
    });
}

function rangeNumber(start, last) {
    let numbers = [];
    for (let i = start; i <= last; i++) {
        numbers.push(i);
    }
    return numbers;
}

let AZ = rangeString('a', 'z') // ['a', ..... 'z']
let AZ = rangeNumber(1, 10) // [1, ..... 10]
```

#### Algorithm
```javascript
function isPrimeSqrt(number) {
    let divisor = 2
  
    while (start <= Math.sqrt(number)) {
        if (number % divisor++ < 1) return false
    }
    return number > 1
}

function isPrime(n){
  let divisor = 2;

  while (n > divisor){
    if(n % divisor == 0){
     return false
    } else
     divisor++
  }
  return true
}

```

#### Tips
```javascript
// clear member in array
// There are different ways to clear array depending on requirement. The results below are for chrome.

array = []; //Fastest
while(array.length > 0) { array.pop(); } //Faster
a.splice(0,a.length) //Slowest
a.length = 0; //Slowest
```
