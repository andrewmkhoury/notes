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

## React element types
What is the difference between React.ReactNode and React.ReactElement types?

- **React.ReactNode**: This type represents anything that can be rendered in React, including strings, numbers, elements, fragments, portals, and even `null` or `undefined`.
- **React.ReactElement**: This type is a more specific type that represents a React element created by `React.createElement` or JSX. It is an object with `type`, `props`, and `key` properties.

**When to use each type**:
- Use **React.ReactNode** when you want to represent any renderable content, including `null` or `undefined`.
- Use **React.ReactElement** when you specifically need to represent a React element object.

I hope this helps clarify the difference! If you have any more questions, feel free to ask.

Source: Conversation with Copilot, 8/8/2024
(1) When to use JSX.Element vs ReactNode vs ReactElement?. https://stackoverflow.com/questions/58123398/when-to-use-jsx-element-vs-reactnode-vs-reactelement.
(2) javascript - Confused between the difference between JSX.Element vs .... https://stackoverflow.com/questions/71473609/confused-between-the-difference-between-jsx-element-vs-react-component-and-when.
(3) Difference between React Component and React Element. https://stackoverflow.com/questions/30971395/difference-between-react-component-and-react-element.
(4) Typescript React.ReactElement vs JSX.Element - Stack Overflow. https://stackoverflow.com/questions/56308756/typescript-react-reactelement-vs-jsx-element.
