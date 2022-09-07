# Adobe Spectrum Library
https://react-spectrum.adobe.com

Spectrum relies on react hooks https://reactjs.org/docs/hooks-intro.html

```
-----------------------
| rendered component  |
-----------------------
| behavior            |
-----------------------
| state               |
-----------------------
```
React Spectrum splits each component into three parts:
* state - bottom of the tech stack.  Implements component logic and returns an interface for reading and updating the component state.
* behavior - platform specific, and depends on the platform API (e.g. the DOM or react-native). 
    Implements  event handling, accessibility, internationalization, etc. — all the
    parts of a component that could be shared across multiple design systems.
    The behavior hook uses the state hook in order to implement component behavior via DOM props.
* rendered component - provides the theme and design system specific logic, and renders the actual platform
    elements (including styles - CSS in classes, CSS-in-JS).

