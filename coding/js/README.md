## Using VIM for JS Development
* https://github.com/sindresorhus/xo - can run it automatically - linter
* https://github.com/vim-syntastic/syntastic - checks syntax 
* https://github.com/sindresorhus/vim-xo - integration of xo w/ vim
* https://github.com/Chiel92/vim-autoformat - autoformat vim

## JavaScript / ECMA Script
Good books:
* [Javascript the Good Parts](https://learning.oreilly.com/library/view/javascript-the-good/9780596517748/) by Doug Crockford

### ES 6
* In ES6 there is a class keyword
* ES6 has backtick quotes for templating 
  ```console.log(`Hello, ${firstName}`)```

### Constants / Globals
* Global variable - check if `window.something` exists before using global
* Use `const` for things that will never be reassigned and "let" for things that will be

#### Imports
require.js - kind of deprecated - complicated and crappy
Module injection uses common.js - require('jquery')
Built in module system - https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import

#### ES6 features
* [Arrows](https://github.com/lukehoban/es6features#arrows) - `=>` defines function sharing lexical this as function body (unlike subfunctions).
* [Classes](https://github.com/lukehoban/es6features#classes) - `class`, `extends`, `constructor`,`get`,`set`, `static` are syntactic sugar over prototypes patterns (i.e. proper-interoperable class definitions).
  ```
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
* [Enhanced Object Literals](https://github.com/lukehoban/es6features#enhanced-object-literals) -
  * set prototype at construction (__proto__ is deprecated but supported)
  * `foo: foo` shorthand
  * dynamically defined property names
    ```
    var obj = {
        // __proto__
        __proto__: theProtoObj,
        // Shorthand for ‘foo: foo’
        foo,
        // Methods
        toString() {
         // Super calls
         return "d " + super.toString();
        },
        // Computed (dynamic) property names
        [ 'prop_' + (() => 42)() ]: 42
    };
    ```
* [Template Strings](https://github.com/lukehoban/es6features#template-strings) - syntactic sugar for concatenating strings
  ```
  // String interpolation and multiline strings
  var name = "Bob", time = "today";
  `Hello ${name}, 
  how are you ${time}?`
  ```

## Floating Point Precision

“JavaScript numbers have plenty of precision and can
          approximate 0.1 very closely. But
          the fact that this number cannot be represented exactly can lead to
          problems. Consider this code:
```
var x = .3 - .2;    // thirty cents minus 20 cents
var y = .2 - .1;    // twenty cents minus 10 cents
x == y              // => false: the two values are not the same!
x == .1             // => false: .3-.2 is not equal to .1
y == .1             // => true: .2-.1 is equal to .1
```

Because of rounding error, the difference between the
          approximations of .3 and .2 is not exactly the same as the
          difference between the approximations of .2 and .1. It is important
          to understand that this problem is not specific to JavaScript: it
          affects any programming language that uses binary floating-point
          numbers”

Excerpt From
JavaScript: The Definitive Guide
David Flanagan

## null vs. undefined
typeof null === "object"
typeof undefined === "undefined"
Both evaluate to false if used as a in the context of a boolean condition in an if, while, etc statement.
https://jsfiddle.net/d9L2vro6/2/
