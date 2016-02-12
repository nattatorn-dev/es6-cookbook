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
##### exmaple 1
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
##### exmaple 2
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
//define and using a template:
const tmpl = addrs => html`
      <table>
      ${addrs.map(addr => html`
          <tr>$${addr.first}</tr>
          <tr>$${addr.last}</tr>
      `)}
      </table>
  `;

//the template is used like this:
console.log(tmpl([
  { first: '<Jane>', last: 'Bond' },
  { first: 'Lars', last: '<Croft>' },
]));

//output:
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
