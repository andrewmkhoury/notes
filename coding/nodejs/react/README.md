# React
* Build complex UIs from “react components”.
* Components tell React what to render.
* When data changes, React updates and re-renders our components.

There are a few different types of components but `React.Component` is most common.
* A component takes in parameters, called props (short for “properties”), and returns a hierarchy of views to display via the render method.

For example:
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
