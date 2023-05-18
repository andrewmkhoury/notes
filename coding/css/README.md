# CSS

## Cascade / Order
* [Cascade](https://web.dev/learn/css/the-cascade/): Algorithm for solving conflicts where multiple rules apply to the same HTML elements
  * Order - Last defined takes precedence
  * Rules that are wrong or not supported are ignored (it falls back instead of failing)
* [Specificity](https://web.dev/learn/css/specificity/): Most specific selector applied with the same rule takes precedence
* [Importance](https://web.dev/learn/css/the-cascade/): Rules with `!important` added to the end take precedence, e.g. `color: red !important;`
```css
.my-element {
  background: green;
  background: purple;
}
```
The backround of elements with class "my-element" are purple, not green.

* Unsupported features fall back to previous cascaded definition:
```css
.my-element {
  font-size: 1.5rem;
  font-size: clamp(1.5rem, 1rem + 3vw, 2rem);
}
```
Browsers that support "clamp" would use the `clamp(1.5rem, 1rem + 3vw, 2rem)`.  Ones that don't would use `1.5rem`.

## Dev tools for debugging CSS
https://web.dev/learn/css/the-cascade/#using-devtools-to-find-out-why-some-css-is-not-applying

## Inheritance
Not all properties inherit but many do, here is a list: https://web.dev/learn/css/inheritance/#which-properties-are-inheritable

`all` lets you override the behavior: 
https://developer.mozilla.org/en-US/docs/Web/CSS/all#syntax

## Selectors
Notes for video: https://www.youtube.com/watch?v=l1mER1bV0N0

CSS selector doc: https://web.dev/learn/css/selectors/

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
```html
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
```html
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
* Pseudo classes - `:hover`, `:focus`, `:required`, `:checked`, `:first-child`, `:last-child`, `:nth-child(3)`, `:nth-child(2n)`, `:nth-child(2n - 1)`, `:nth-last-child(2n - 1)`, `:only-child`, `:last-of-type`, `:nth-of-type`, `:not(.selector)` etc. - see [here](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes)
```html
<style>
  li:hover {
    color: red;
  }
  li:not(.skip) {
    text-decoration: underline;
  }
  li:nth-child(2n) {
    background-color: gray;
  }
</style>
<ul>
  <li>Underlined, red when hovered by mouse</li>
  <li>Underlined, gray bg, red text when hovered by mouse</li>
  <li>Underlined, red when hovered by mouse</li>
  <li>Underlined, Gray bg, red text when hovered by mouse</li>
  <li class="skip">Red when hovered by mouse</li>
  <li>Underlined, gray bg, red text when hovered by mouse</li>
</ul>
```
* Pseudo elements: `:before`, `:after`
```html
<style>
  div.red:before {
    content: "Before";
    background-color: red;
  }
</style>
<div class="red">
CSS will add red text "Before" this.
</div>
```
* Data attributes - wrap with brackets `[` `]`
```html
<style>
  [data-color] {
    background-color: red;
  }
  [data-color="lightskyblue"] {
    background-color: lightskyblue;
  }
</style>
<div data-color>
This has a red background
</div>
<div data-color="lightskyblue">
This has a light sky blue background
</div>
```
