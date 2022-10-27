# Adobe React Spectrum Library
https://react-spectrum.adobe.com

## Architecture
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

### Implementation
* Split into 3 npm scopes - @react-spectrum, @react-aria, @react-stately
* Individually versioned packages for each component.  i.e. use only what you need.
* Each component is highly composable - features are split into multiple hooks.  Combine them to achieve what you need.

3 Scopes:
* React Stately - implements state management and core logic for each component. 
* React Aria - implements behavior and accessibility for the web according to WAI-ARIA Authoring Practices. Full screen reader and keyboard navigation support, along with mouse and touch interactions.
* React Spectrum - puts all of these pieces together and implements the Adobe-specific styling.  Supports theming, dark mode and responsive scaling.
