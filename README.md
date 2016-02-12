# React-Redux-ES6-Cookbook
Recipes for making your React.js Components Awesome

#### Let, Const

```ruby

  let count = 0;
  console.log(count);  // 0
  const API_KEY = 'KEY';
  API_KEY = 'NEW_KEY'; // ERROR! "API_KEY" is read-only
console.log(count);  // count is not defined
```
#### Arrow Function

###### Shorter functions
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
