# React-Redux-ES6-Cookbook
Recipes for making your React.js Components Awesome

# Table of Contents
1. [Let, Const](#let-const)
2. [Arrow Function](#arrow-function)
3. [Template Strings](#template-stringst)
4. [Classes](#classes)
5. [Spread Operator](#spread-operator)
6. [Union, Intersection, Difference](#union-intersection-difference)
7. [Map](#map)
8. [Promise](#promise)
9. [Default, Rest, Spread](#default-rest-spread)
10. [Destructuring](#destructuring)

#### Let, Const
```javascript

let count = 0;
console.log(count);  // 0
const API_KEY = 'KEY';
API_KEY = 'NEW_KEY'; // ERROR! "API_KEY" is read-only

console.log(count);  // count is not defined
```
#### Arrow Function
![Arrow Function](http://www.uxebu.com/wp-content/uploads/2015/05/arrow-function4-150px-150x134.jpg)
##### exmaple 1
```javascript
arr.map(val => val * 2)

// instead of
arr.map(function(val) { return val * 2 })

const isThree = num => num === 3;
const containsThree = arr => !!arr.find(item => item === 3);
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
#### Classes
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
#### Spread Operator
```javascript
let params = [ "hello", true, 7 ]
let other = [ 1, 2, params ] // [ 1, 2, "hello", true, 7 ]
f(1, 2, params) === 9

let str = "foo"
let chars = [str] // [ "f", "o", "o" ]
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

#### Promise
#### Example 1
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
##### Default, Rest, Spread
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

##### Destructuring
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
