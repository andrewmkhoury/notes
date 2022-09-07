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
