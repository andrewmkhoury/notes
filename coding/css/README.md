# CSS

## Selectors
* Universal selector - `*` selects all elements
```
* {
}
```
* Element selector - `div`, `li`, etc. name of the tag
```
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
```
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
```
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
```
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
```
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
```
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
```
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
</div>
```
