# Number and `Math` features

## Binary and Octal Numbers

Integers can now be described in binary and octal notation.

From this:

```javascript
// All are equal to 255.
var decimalES5 = 255;
var hexadecimalES5 = 0xFF;
var binaryES5 = undefined;
var octalES5 = undefined;
```

To this:

```javascript
// All are equal to 255.
let decimalES6 = 255;
let hexadecimalES6 = 0xFF;
let binaryES6 = 0b11111111;
let octalES6 = 0o377;
```

## New properties for `Number`

`isFinite`, `isNaN`, `parseFloat` and `parseInt` are all available
in ES5 globally. Now they have also been added to `Number`. So you can do both `isFinite(Infinity)` and `Number.isFinite(Infinity)`. 

The only difference is that `Number.isFinite()` and `Number.isNaN()` will not coerce (change) the data it receives into a number. As in, it
will not turn a string `'123'` into a number `123`.

From this:

```javascript
console.log(isFinite('123'));
// --> true
console.log(Number.isFinite('123'));
// ->- false
```

## `Number.EPSILON`

`Number.EPSILON` used to compare floating point numbers with a tolerance
for rounding errors. JavaScript struggles to represent decimal points
with accuracy where `0.1` and `0.2` aren't actually precise numbers
in the language.

```javascript
console.log(0.1 + 0.2 === 0.3);
// --> false (lol JavaScript)
```
What `Number.EPSILON` says is 'calculate this, but here is a reasonable
margin of error to account for your difficulty in representing these
numbers, lol'. 

```javascript
console.log(Math.abs((0.1 + 0.2) - 0.3) < Number.EPSILON);
// --> true
```

_I don't really get how this works..._

**TODO: Get something/someone to explain this to me**

## `Number.isInteger`

We can now tell if a number is an integer or not.

```javascript
console.log(Number.isInteger(2));
// --> true
console.log(Number.isInteger(3.4));
// --> false
```

## Determine if an Integer is safe

A new method for determining if JS integer is safe, where safety is
achieved if the the number is within the signed 53 bit range where
there will be no loss of number precision. _OoooOooo, this is very cool_.

JavaScript numbers only have enough space to represent 53 bit signed
integers. After the 53 bit limit is reached, two or more integers
are represented as the same integer. JavaScript will only be able
to represent every second mathematical integer. Safe numbers are the
ones when JavaScript can represent every single Integer.

```javascript
let smallInteger = 90071;
let largeInteger = 9007199254740992;
console.log(Number.isSafeInteger(smallInteger));
console.log(Number.isSafeInteger(largeInteger));
```

## New `Math` methods

`Math.sign` returns the sign of a number.

```javascript
console.log(Math.sign(-87));
// -> '-1'
```

`Math.trunc` removes the decimal fraction of a number.

```javascript
console.log(Math.trunc(27.89));
// --> 27
```

`Math.cbrt` returns the cube root of a number.

```javascript
console.log(Math.cbrt(9));
// --> 3
```

`Math.log2` computes the logarithm to base 2.

```javascript
console.log(Math.log2(8));
// --> 2
```

`Math.log10` computes the logarithm to base 10.

```javascript
console.log(Math.log10(100));
// --> 2
```

_TIL: Twitter had to switch from integers to strings when tweet IDs
became too large in its JSON API because integers only had a range of 53 bits when they needed 64. Support is planned in JavaScript for
large numbers_
