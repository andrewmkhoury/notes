# CSS

## Selectors
* Universal selector - `*` selects all elements
```html
<html>
  <head>
    <style>
    * {
      color:red;
    }
    </style>
  </head>
  <body>
    all text is red
  </body>
</html>
```
* Element selector - `div`, `li`, etc. name of the tag
```html
<style>
div {
  color: green;
}
</style>
<div>
This text is green.
</div>
```
* Class selector - `.classname`
```html
<style>
.red {
  color: red;
}
</style>
<div class="red">
This text is red.
</div>
```
* id selector - `#idname`
```html
<style>
#mydiv {
   color: gray;
}
</style>
<div id="mydiv">
This text is gray.
</div>
```
* element + class combined
```html
<style>
div.red {
  color: red;
}
</style>
<div class="red">
This text is red.
</div>
<span class="red">
This text is NOT red.
</span>
```
* element + multi-class - chained `.`
```html
<style>
div.red-bg.green-text {
  background-color: red;
  color: green;
}
</style>
<div class="red-bg green-text">
Background is red, text is green.
</div>
<span class="red-bg">
This text is NOT styled.
</span>
```
* multiple OR'ed selectors - `,`
```html
<style>
div.red, span.red {
  color: red;
}
</style>
<div class="red-bg green-text">
This text is red.
</div>
<span class="red">
This text is red.
</span>
```
* Direct child - `>`
```html
<style>
div > div.red {
  color: red;
}
</style>
<div class="red">
 This text is NOT red.
  <div class="red">
  This text is red.
  </div>
  <div>
    <div class="red">
    This text is NOT red.
    </div>
  </div>
</div>
```
* Any child - ` `
```html
<style>
div > div.red {
  color: red;
}
</style>
<div class="red">
 This text is NOT red.
  <div class="red">
  This text is red.
  </div>
  <div>
    <div class="red">
    This text is red.
    </div>
  </div>
</div>
```
* Siblings after element - `~`
```
<style>
  li.red ~ li {
    color: red;
  }
</style>
<ul>
  <li>Not red</li>
  <li>Not red</li>
  <li class="red">Not red</li>
  <li>Red</li>
  <li>Red</li>
  <li>Red</li>
  <li>Red</li>
  <li>Red</li>
</ul>
```
* Only next sibling after element - `+`
```
<style>
  li.red + li {
    color: red;
  }
</style>
<ul>
  <li>Not red</li>
  <li>Not red</li>
  <li class="red">Not red</li>
  <li>Red</li>
  <li>Not red</li>
  <li>Not red</li>
  <li>Not red</li>
  <li>Not red</li>
  <li>Not red</li>
</ul>
```
* Pseudo selectors - `:hover`, `:focus`, `:required`, `:checked` - see [here](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes)
```
<style>
  li:hover {
    color: red;
  }
</style>
<ul>
  <li>Red when hovered by mouse</li>
  <li>Red when hovered by mouse</li>
  <li>Red when hovered by mouse</li>
  <li>Red when hovered by mouse</li>
  <li>Red when hovered by mouse</li>
  <li>Red when hovered by mouse</li>
</ul>
```
