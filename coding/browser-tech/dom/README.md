# DOM

## Element.previousElementSibling
https://developer.mozilla.org/en-US/docs/Web/API/Element/previousElementSibling

```html
<div>
  <div id="a"></div>
  <div id="b"></div>
  <div id="c"></div>
</div>
```
```javascript
var elemB = document.getElementById("b");
var elemA = elemB.previousElementSibling;
console.log(elemA.id);
```
Output:
```
a
```
