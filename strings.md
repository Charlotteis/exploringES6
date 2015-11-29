# New string features

## New Methods

`startsWith()` determines whether the string you're looking for
exist at the start of the string.

```javascript
console.log('charlotte is amazing'.startsWith('char'));
// --> true
```

`endsWith()` determines whether the string you are looking for
exist at the end of a string.

```javascript
console.log('charlotte is amazing'.endsWith('ing'));
// --> true
```

`includes()` determines whether the string you are looking for
are contained within the provided string.

```javascript
console.log('charlotte is amazing').includes('poop');
// --> false
```

`repeat()` takes the string and outputs a new string where the "old"
string is repeated based on the number you provided.

```javascript
console.log('🍰'.repeat(8));
// --> '🍰🍰🍰🍰🍰🍰🍰🍰'
```

## The template literal

We can now do easier string interpolation using the template literal.

From this:

```javascript
var cats = '3';
console.log('My name is Charlotte and I want ' + cats + ' cats.');
// --> 'My name is Charlotte and I want 3 cats.'
```

To this:

```javascript
let cats = '3';
console.log(`My name is Charlotte and I want ${cats} cats.`);
// --> 'My name is Charlotte and I want 3 cats.'
```

We can also do multi-line strings in an easier way.

From this:

```javascript
var poem = 
  'I love to write\n' +
  'great poetry\n' +
  'and rhymes that\n' +
  'don\'t quite\n' +
  'work for me\n';
```

To this:

```javascript
let poem = `
I love to write
great poetry
and rhymes that
don't quiet
work for me`;
```

_Note we are not using '' but a ``._

## String iteration

Strings are iterable so you can use the `for-of` loop.

```javascript
for (let character of 'batman') {
    console.log(character);
}
// -> b a t m a n (each character on a new line)
```

You can use the spread operator (`...`) to turn a string into an
array of characters.

```javascript
let array = [...'batman'];
console.log(array);
// --> ['b', 'a', 't', 'm', 'a', 'n']
```
