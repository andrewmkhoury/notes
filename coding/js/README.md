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
