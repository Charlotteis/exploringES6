# Deploying ES6

* Compiling from ES6 to ES5 will be the only option for a while.
* Do it before deployment (statically) or at runtime (dynamically)

## Native use

* Check the environment (browser) to see if it can accept ES6, if so then
use the ES6 file. Else, use the transpiled ES5 file.
    - _You'd have to do so many if/else feature detection checks_

## Transpile

* Transpilers: TypeScript, Traceur, Babel.
    - If before deployment, use a built tool like grunt/gulp or just call
    the transpiler on your code.
* Package managers: npm, bower, jspm.
* Module system: RequireJS, Browserify, webpack, SystemJS.

## Some ES6 features cannot be transpiled

* Brand new features cannot be transpiled completely faithfully
    - `let` and `const` are transpiled to∏ var. Any variables using the name `let/var` will be renamed to avoid clashes. No way to have the
    immutable bindings of const in ES5.

* Proxies, subclassable built-in constructors (Error, Array) and tail
call optimisation cannot be transpiled at all.

_Lots more about webpack and npm and other stuff that I won't lease
space in my head to, until I actually need/want to use ES6 somewhere that
requires dynamic (in real time) compilation. I'm a fan of static
(before deployment) transpilation, it seems quicker_
