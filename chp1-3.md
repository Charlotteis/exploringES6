# About ES6

* ES6 Became standard in June 2015
    - _I guess this means ES6 really wont be the standard for a few years_
* 'Transpilers' (Babel, Traceur) compile funky ES6 to ES5
* ES7 already in the works (a.k.a ES 2016)
* Plan is to release a new version of ECMAScript every year, with whatever
is ready at the time.
    - _Sounds like they could use some proper semantic versioning, rather
    than upping the major version each time_

* Stakeholders of the web
    - Creators of JavaScript engines
    - Developers
    - Users
 
* For engines, ES6 will be a superset of ES5. Nothing will be removed.
* Will take years before the mainstream are no longer using an ES5 engine,
so best shot is to use transpilers.

# ES6 FAQ

* Implementation table of ES6 accross engines: http://kangax.github.io/compat-table/es6/
    - _Not looking very good right now. I wonder how long it will take._
* All ES5 code is ES6 code, no migration necessary. It will all still work.
* Some features not created for "normal programmers" but for library authors
    - Like generators, iterators and proxies. Normal programmers could
    know they exists but it's not overly important for them.

# One JavaScript: Avoiding versioning ES6

_If the goal is to avoid versioning... why do we have new names each year? Call it ECMAScript and be done with it. Also get the rights to the name 'JavaScript' from Oracle pls._

* Strict mode occurs when you put `'use strict'` at the start of your .js
    - Forbids certain syntax (e.g. `with`)
    - Functions can only be defined at the top level of a scope
    - More reserved names for variables (e.g. `let`, `package`, `private`)
    - More errors:
        - Assigning to undeclared variable causes ReferenceError.
            - If you did this in non-strict, a global variable would be
            automatically created
            - **TODO: Find out why this was restricted**
        - Changing read-only properties raises TypeError
            - e.g. `string.length = 80.` 🙅🏽
* Adoption is low: breaks existing code and it can slow down execution

* `let` functionality hard to add into non-strict mode because `let` is
not a restricted variable word. 
* The bodies of modules and classes are implicitly in strict mode in ES6
    - If all code will exist in modules in the future, all code will be
    upgraded to using strict mode

* 'One JavaScript' (backwards compatibility) means we can't fix existing 'quirks'. e.g. `typeof null` will always return `object` instead of `null`.
