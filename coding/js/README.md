# JavaScript Notes
## Syntax
### == vs ===
* == only compares values
* === compares values + type

Example:

```
console.log(false == '0')
console.log(false === '0')
```

Output
```
true
false
```

### NaN

NaN is returned for math operations with non-numeric operands or division by zero. 

Testing for NaN:

Pre-ECMA6:
```
value !== value
```
ECMA6:
```
Number.isNaN()
```
### Scope

Lexical:

```
var downloadManager = {
  initialize: function() {
    var _this = this; // Set up `_this` for lexical access
    $('.downloadLink').on('click', function () {
      _this.startDownload();
    });
  },
  startDownload: function(){
    this.thinking = true;
    // request the file from the server and bind more callbacks for when it returns success or failure
  }
  //...
};
```

Bound:

```
var downloadManager = {
  initialize: function() {
    $('.downloadLink').on('click', function () {
      this.startDownload();
    }.bind(this)); // create a function object bound to `this`
  }
//...
```

### Closure

Inner function which can acccess variables in the outer (enclosing) function’s scope chain. The closure has access to variables in three scopes; specifically: (1) variable in its own scope, (2) variables in the enclosing function’s scope, and (3) global variables.
```
var globalVar = "xyz";

(function outerFunc(outerArg) {
  var outerVar = 'a';
  
  (function innerFunc(innerArg) {
    var innerVar = 'b';
    
    console.log(
      "outerArg = " + outerArg + "\n" +
      "innerArg = " + innerArg + "\n" +
      "outerVar = " + outerVar + "\n" +
      "innerVar = " + innerVar + "\n" +
      "globalVar = " + globalVar);
    
  })(456);
})(123);
```

Output

```
outerArg = 123
innerArg = 456
outerVar = a
innerVar = b
globalVar = xyz
```

### Objects in JS

## Important points
### null is an object
```null``` is an object so ```(typeof bar === "object")``` evaluates to ```true```
### Accidental globals
```function () { var a = b = 3; }``` has b as a global variable and a as a local.  To have both as local ```function () { var a = 3; var b = a; }```.  In ECMAScript5 ```use strict``` mode, the js engine would throw b is undefined if you tried to execute ```use strict; function () { var a = b = 3; }```.
### this and closures
In the inner function call / closure, this.foo is undefined and self.foo === "bar" because it no longer refers to myObject.

```
var myObject = {
    foo: "bar",
    func: function() {
        var self = this;
        console.log("outer func:  this.foo = " + this.foo);
        console.log("outer func:  self.foo = " + self.foo);
        (function() {
            console.log("inner func:  this.foo = " + this.foo);
            console.log("inner func:  self.foo = " + self.foo);
        }());
    }
};
myObject.func();
```
### wrapping scripts with function / closure
It is popular to wrap scripts with a function call which creates a closure around the code.  This creates a separate namespace for the code so there aren't clashes between object and function names in different libraries.  For example this is used for jQuery like this:

```(function($) { /* jQuery plugin code referencing $ */ } )(jQuery);```
### use strict mode of ECMAScript5
"use strict" is used in javascript to:
* Makes debugging easier - it makes code errors that would have been ignored before throw errors.
* Prevents accidental global variables - it disallows variable declarations without "var".  Usually when you declare a variable without using var it makes it a global variable.
* Eliminates this coercion - Without use strict, when ```this``` is ```null``` or ```undefined``` then the interpreter would be coerced to the global object.  In strict mode, referring to null or undefined ```this``` throws an error.
* Makes eval() safer - In non-strict mode, eval variables are created in the containing scope.  In non-strict mode, variables won't get attached to the global scope. For example:
  
  ```
  var x = 17;
  var evalX = eval("'use strict'; var x = 42; x");
  console.assert(x === 17);
  console.assert(evalX === 42);
  ```
* Throws error on invalid usage of delete - delete operator (used to remove properties from objects) cannot be used on non-configurable properties of the object.  In non-strict mode it fails silently.

### JS Numbers
The output of the code below is unpredictable
```
console.log(0.1 + 0.2);
console.log(0.1 + 0.2 == 0.3);
```
That is because all numbers in javascript are treated with floating point precision.
### Testing if number is an Integer
You can test if a number is an integer with this function.  ^ is operator for XOR and only works on signed 32-bit integers in two complement format.
```
function isInteger(x) { return (x^0) === x; } 
```
The following solution would also work, although not as elegant as the one above:
```
function isInteger(x) { return Math.round(x) === x; }
```
### How to write a method that adds numbers such that you can call it both of these ways sum(2,3) or sum(2)(3)
Answer 1
```
function sum(x) {
  if (arguments.length == 2) {
    return arguments[0] + arguments[1];
  } else {
    return function(y) { return x + y; };
  }
}
```
Answer 2
```
function sum(x, y) {
  if (y !== undefined) {
    return x + y;
  } else {
    return function(y) { return x + y; };
  }
}
```
### Variable

```
var arr1 = "john".split('');
var arr2 = arr1.reverse();
var arr3 = "jones".split('');
arr2.push(arr3);
console.log("array 1: length=" + arr1.length + " last=" + arr1.slice(-1));
console.log("array 2: length=" + arr2.length + " last=" + arr2.slice(-1));
```
Outputs
```
array 1: length=5 last=j,o,n,e,s
array 2: length=5 last=j,o,n,e,s
```
arr2 is just a reference to arr1 and array.push(['j','o','n','e','s']) adds the array ['j','o','n','e','s'] as a single item to the end of the array.

### Addition and Subtraction

```
console.log(1 +  "2" + "2");
console.log(1 +  +"2" + "2");
console.log(1 +  -"1" + "2");
console.log(+"1" +  "1" + "2");
console.log( "A" - "B" + "2");
console.log( "A" - "B" + 2);
```

Output:

```
"122"
"32"
"02"
"112"
"NaN2"
NaN
```

### Avoiding stack overflow

```
var list = readHugeList();

var nextListItem = function() {
    var item = list.pop();

    if (item) {
        // process the list item...
        nextListItem();
    }
};
```

Use setTimeout
```
var list = readHugeList();

var nextListItem = function() {
    var item = list.pop();

    if (item) {
        // process the list item...
        setTimeout( nextListItem, 0);
    }
};
```

### 

```
for (var i = 0; i < 5; i++) {
  setTimeout(function() { console.log(i); }, i * 1000 );
}
```

Output
```
5
5
5
5
5
```

This can be fixed by using a closure:
```
for (var i = 0; i < 5; i++) {
  (function(x) {
    setTimeout(function() { console.log(x); }, x * 1000 );
  })(i);
}
```

### || and &&

```
console.log("0 || 1 = "+(0 || 1));
console.log("1 || 2 = "+(1 || 2));
console.log("0 && 1 = "+(0 && 1));
console.log("1 && 2 = "+(1 && 2));
```

Output:

```
0 || 1 = 1
1 || 2 = 1
0 && 1 = 0
1 && 2 = 2
```

### Associative array keys

```
var a={},
    b={key:'b'},
    c={key:'c'};

a[b]=123;
a[c]=456;

console.log(a[b]);
```

Output:

```
456
```

Object properties are stringified so both b and c are "[object Object]"

### Function context

```
var hero = {
    _name: 'John Doe',
    getSecretIdentity: function (){
        return this._name;
    }
};

var stoleSecretIdentity = hero.getSecretIdentity;

console.log(stoleSecretIdentity());
console.log(hero.getSecretIdentity());
```

Output

```
undefined
John Doe
```

Solution

```
var stoleSecretIdentity = hero.getSecretIdentity.bind(hero);
```

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

> Because of rounding error, the difference between the
          approximations of .3 and .2 is not exactly the same as the
          difference between the approximations of .2 and .1. It is important
          to understand that this problem is not specific to JavaScript: it
          affects any programming language that uses binary floating-point
          numbers”

> -- Excerpt From
JavaScript: The Definitive Guide
David Flanagan

## null vs. undefined
```
typeof null === "object"
typeof undefined === "undefined"
```
Both evaluate to false if used as a in the context of a boolean condition in an if, while, etc statement.
https://jsfiddle.net/d9L2vro6/3/

## Nullish coalescing operator
```
const foo = null ?? 'default string';
console.log(foo);
// expected output: "default string"

const baz = 0 ?? 42;
console.log(baz);
// expected output: 0
```
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_operator
