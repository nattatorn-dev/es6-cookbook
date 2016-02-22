# React-Redux-ES6-Cookbook
Recipes for making your React.js Components Awesome

# Table of Contents
1. [Let, Const](#let-const)
2. [Arrow Function](#arrow-function)
3. [Template Stringst](#template-stringst)
4. [Classes](#classes)
5. [Spread Operator](#spread-operator)
6. [Union, Intersection, Difference](#union-intersection-difference)
7. [Map](#map)
8. [Promise](#promise)

#### Let, Const
```ruby

let count = 0;
console.log(count);  // 0
const API_KEY = 'KEY';
API_KEY = 'NEW_KEY'; // ERROR! "API_KEY" is read-only

console.log(count);  // count is not defined
```
#### Arrow Function
![Arrow Function](http://www.uxebu.com/wp-content/uploads/2015/05/arrow-function4-150px-150x134.jpg)
##### exmaple 1
```ruby
arr.map(val => val * 2)

// instead of
arr.map(function(val) { return val * 2 })

const isThree = num => num === 3;
const containsThree = arr => !!arr.find(item => item === 3);
```
##### exmaple 2
```ruby
var a = [
  "Hydrogen",
  "Helium",
  "Lithium",
  "Beryl­lium"
];

var a2 = a.map(function(s){ return s.length });

var a3 = a.map( s => s.length );
```
##### exmaple 3
```ruby
// normal
function(arg) {
  // do something
}

// Use arrow function
(arg) => {
  // do something
}

// share the same this as surrounding code.
var bob = {
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

#### Template Strings
##### exmaple 1
```ruby
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
##### exmaple 2
```ruby
const name = 'Suranart';

const message = `Hello! "${name}".`;

// equivalent to
// const message = "Hello! \"" + name + "\".";

console.log(message);
const name = 'Suranart';

const message = `Hello! "${name}".`;

// equivalent to
// const message = "Hello! \"" + name + "\".";

console.log(message);
```
#### Classes
##### exmaple 1
```ruby
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
```ruby
let params = [ "hello", true, 7 ]
let other = [ 1, 2, params ] // [ 1, 2, "hello", true, 7 ]
f(1, 2, params) === 9

let str = "foo"
let chars = [str] // [ "f", "o", "o" ]
```
#### Union, Intersection, Difference
```ruby
// union
let a = new Set([1,2,3]);
let b = new Set([4,3,2]);
let union = new Set([...a, ...b]);
// {1,2,3,4}

// intersection
let a = new Set([1,2,3]);
let b = new Set([4,3,2]);
let intersection = new Set(
[...a].filter(x => b.has(x)));
// {2,3}

// difference
let a = new Set([1,2,3]);
let b = new Set([4,3,2]);
let difference = new Set(
[...a].filter(x => !b.has(x)));
// {1}

[credit: Dr. Axel Rauschmayer](http://www.2ality.com/2015/01/es6-set-operations.html)
```
#### Map
##### Exmaple 1 (Basic operations, size, clear and chainable)
```ruby
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
```ruby

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

//multi task
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
```ruby
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
