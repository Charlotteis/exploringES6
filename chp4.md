# Trying out ES6

Three methods of playing with ES6:

* Use online Babel REPL: http://babeljs.io/repl/
* Use babel-node on the command line
* Use some parts natively in some JS engines

# New features

## `var` -> `let/const`

* `let` = block-scoped version of `var`. True local scoping.
* `const` = like let, but creates constants where its value cant be changed

## String interpolation

From this:

```javascript
var name = prompt('What is your name?');

console.log('Hello ' + name + ', how are you?');
// --> "Hello ES5, how are you?"
```

To this:

```javascript
let name = prompt('What is your name?');

console.log(`Hello ${name}, how are you?'`)
// --> "Hello ES6, how are you?"
```

## Multi-line strings

From this:

```javascript
var widget = 
  '<div id="es5">\n' +
  '  <span>I love ES5</span>\n' +
  '</div>\n';
```

To this:

```javascript
const widget = `
  <div id="es6">
    <span>I love ES6</span>
  </div>`;
```

## Function expressions -> Arrow Functions

_I might have this wrong... get it?._

**TODO: Explore this further**

`this` can be tricky to use. In ES5, we usually try and make this easier
by explicitly assigning `this` to a variable (_known as shadowing?_).

```javascript
var _this = this;

widget.addEventListener('click', function() {
  console.log(_this);
})
```

Now we can use arrow functions which don't shadow `this`:

```javascript
widget.addEventListener('click', () => {
  console.log(this);
})
```

_This appears to be a lot about verbosity. I prefer to be verbose here
and am unlikely to adopt arrow functions._

## Multiple return values

If a method returns multiple values, in order to use them elsewhere
you used to have to assign the values explicitly. Now we can simplify this assignment.

From this:

```javascript
function printArray() {
  return [1, 2, 3];
}

var one = printArray[0];
var two = printArray[1];
var three = printArray[2];

console.log(one, two, three);
// -> 1 2 3
```

To this:

```javascript
function printArray() {
  return [1, 2, 3];
}

let [one, two, three] = printArray();
console.log(one, two, three);
// -> 1 2 3
```

### `for`/`forEach` -> `for-of`

The advantage of `for` is that you can break from within it if necessary. `forEach` cannot do that, but it is more concise than a `for` loop. `for-of` is syntactically smaller and you can break from within it.

From this:

```javascript
var myArray = ['i', 'love', 'javascrippies!', '✨'];

for (var i = 0; i < myArray.length; i++) {
  if (myArray[i] === '✨') {
    break;
  } else {
    console.log(myArray[i]); 
  }
}

// --> 'i'
// --> 'love'
// --> 'javascrippies!'

// OR
var myArray = ['i', 'love', 'javascrippies!', '✨'];

myArray.forEach(function(item) {
  console.log(item);
})

// --> 'i'
// --> 'love'
// --> 'javascrippies!'
// --> '✨'
```

To this:

```javascript
let myArray = ['i', 'love', 'javascrippies!', '✨'];

for (let item of myArray) {
  if (item === '✨') {
    break;
  } else {
    console.log(item); 
  }
}
```

## Default parameters

Sometimes you want to define default values for a method.

From this:

```javascript
function add(x, y) {
  var x = x || 2;
  var y = y || 2;

  console.log(x + y);
}

add(5, 2);
// --> 7
add();
// --> 4
add();
// --> 4
```

To this:

```javascript
function add(x=2, y=2) {
    console.log(x + y);
}

add(20, 4);
// --> 24
add();
// --> 4
add();
// --> 4
```

## Named parameters

**TODO: Find another explanation elsewhere**

## `arguments` -> rest parameters

**TODO: Find another explanation elsewhere**

## `apply()` -> spread (`...`)

**TODO: Find another explanation elsewhere**

## `concat()` -> spread (`...`)

To combine arrays in ES5, you'd used the `concat()` method. Now, you
can use the spread `...` operator.

From this:

```javascript
var array1 = ['i', 'love'];
var array2 = ['javascrippies!', '✨'];

console.log(array1.concat(array2));
// --> ['i', 'love', 'javascrippies!', '✨']
```

To this:

```javascript
let array1 = ['i', 'love'];
let array2 = ['javascrippies!', '✨'];

console.log([...array1, ...array2])
```

## Updated classes

Better and cleaner syntax.

From this:

```javascript
function Cake(type) {
  this.type = type;
}

Cake.prototype.describe = function() {
  return 'My ' + this.type + ' cake is delicious!';
}

var birthday = new Cake('banoffee');
console.log(birthday.describe());
// --> 'My banoffee cake is delicious!'
```

To this:

```javascript
class Cake {
  constructor(type) {
    this.type = type;
  }

  describe() {
    return `My ${this.type} cake is delicious!`;
  }
}

let birthday = new Cake('banoffee');
console.log(birthday.describe());
// --> 'My banoffee cake is delicious!'
```

## Class Inheritance

In many cases, you'll create different classes that inherit from a
'super' class. E.g. There is a 'Cake' super class, and many different
types of cakes (Birthday Cake, Wedding Cake) that share some of the 
same properties as a regular Cake (ingredients, icing) but also have
their own properties (tiers, candles). 🍰

To do this in ES5 you need extensive use of `prototype` and lines of
code not contained anywhere nice but lying outside of the original
Class construction. In ES6 we have simpler inheritance using `extends` and also a nicer syntax where the properties of a Class remain
contained within the original construction of the Class.

From this:

```javascript
function Cake(type) {
  this.type = type;
}

Cake.prototype.describe = function() {
  return 'My ' + this.type + ' cake is delicious!';
}

function BirthdayCake(type, name) {
  Cake.call(this, type);
  this.name = name;
}

BirthdayCake.prototype = Object.create(Cake.prototype);
BirthdayCake.prototype.constructor = BirthdayCake;
BirthdayCake.prototype.describe = function() {
  return Cake.prototype.describe.call(this)
    + ' I hope you enjoy this, ' + this.name +'!';
};

var charlottesCake = new BirthdayCake('lemon', 'Charlotte');
console.log(charlottesCake.describe() + ' 🎂');
// --> 'My lemon cake is delicious! I hope you enjoy this, Charlotte! 🎂'
```

To this:

```javascript
class Cake {
  constructor(type) {
    this.type = type;
  }

  describe() {
    return `My ${this.type} cake is delicious!`;
  }
}

class BirthdayCake extends Cake {
  constructor(type, name) {
      super(type);
      this.name = name;
  }

  describe() {
    return super.describe() + ` I hope you enjoy this, ${this.name}!`;
  }
}

let charlottesCake = new BirthdayCake('lemon', 'Charlotte');
console.log(charlottesCake.describe() + ' 🎂');
// --> 'My lemon cake is delicious! I hope you enjoy this, Charlotte! 🎂'
```

* Note: What once was impossible, we can now extend the built-in error
constructor in a nice way, too.

## Defining functions in an object literal

From this:

```javascript
var pokemon = {
  charmander: function() {
    console.log('I am the base pokemon!');
  },
  charmeleon: function() {
    console.log('I am the level 2 evolved Charmander!');
  },
  charizard: function() {
    console.log('I am the last stage of Charmander evolution!');
  }
}

pokemon.charizard();
// --> 'I am the last stage of Charmander evolution!'
```

To this:

```javascript
let pokemon = {
  charmander() {
    console.log('I am the base pokemon!');
  },
  charmeleon() {
    console.log('I am the level 2 evolved Charmander!');
  },
  charizard() {
    console.log('I am the last stage of Charmander evolution!');
  }
}

pokemon.charizard();
// --> 'I am the last stage of Charmander evolution!'
```

## From objects to Maps

**TODO: Find another explanation elsewhere**
