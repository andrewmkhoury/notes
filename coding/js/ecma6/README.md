# ECMA6
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

* [Spread operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)
The spread operator `...` is a feature of JavaScript introduced with ES6 that gives you access to the insides of an iterable object. An "iterable object" is anything you can iterate over item by item, such as arrays, objects literals, and strings. These kinds of JavaScript types can be traversed in some sequential fashion1.

```
const numbers = [1, 2, 3];

console.log(sum(...numbers));
// Expected output: 6
```

* [Destructuring assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)
```
[a, b, ...rest] = [10, 20, 30, 40, 50];

console.log(rest);
// Expected output: Array [30, 40, 50]
```
