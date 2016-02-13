# React-Redux-ES6-Cookbook
Recipes for making your React.js Components Awesome

# Table of Contents
1. [Let, Const](#Let,-Const)
3. [Spread Operator](#####Spread-Operator)

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
