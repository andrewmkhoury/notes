# React
* Build complex UIs from “react components”.
* Components tell React what to render.
* When data changes, React updates and re-renders our components.

Tutorial: https://react.dev/learn

There are a few different types of components but `React.Component` is most common.
* A component takes in parameters, called props (short for “properties”), and returns a hierarchy of views to display via the render method.
* Markup and JS are in the same file loosely coupled in components.
* The syntax below where the `<div ...>` is directly in the JavaScript is called "jsx".  For the internals of how react JSX plugin for babel compiler/transformer library works, see [here](https://babeljs.io/docs/en/babel-plugin-transform-react-jsx)
* When JSX tags are added they get compiled down to React.createElement calls by the babel react jsx plugin.  See [here](https://reactjs.org/docs/react-without-jsx.html) for what react looks like without the JSX.

Older style of react component using classes - example React + JSX code:
```javascript
class ShoppingList extends React.Component {
  render() {
    return (
      <div className="shopping-list">
        <h1>Shopping List for {this.props.name}</h1>
        <ul>
          <li>Instagram</li>
          <li>WhatsApp</li>
          <li>Oculus</li>
        </ul>
      </div>
    );
  }
}

// Example usage: <ShoppingList name="Mark" />
```

Newer style using functions:
```javascript
function MyButton() {
  return (
    <button>
      I'm a button
    </button>
  );
}

export default function MyApp() {
  return (
    <div>
      <h1>Welcome to my app</h1>
      <MyButton />
    </div>
  );
}
```
