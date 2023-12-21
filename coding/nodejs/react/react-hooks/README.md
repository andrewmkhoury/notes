# React Hooks
* Related Doc https://react.dev/reference/react/hooks
* Excellent video tutorial on react hooks: https://www.youtube.com/watch?v=TNhaISOUy6Q

* **State** - declares a [state variable](https://react.dev/learn/state-a-components-memory) that you can update directly.
  * Call `useState` at the top level of your component to declare a state variable.
  * e.g. `const [name, setName] = useState('Taylor');`
* **Context** - Context lets a component receive information from distant parents without passing it as props.
  * `useContext` reads and subscribes to a context.
  * e.g. `const theme = useContext(ThemeContext);`
* **Ref** - Refs let a component hold some information that isn’t used for rendering.
  * Refs are an “escape hatch” from the React paradigm. They are useful when you need to work with non-React systems, such as the built-in browser APIs.
  * `useRef` declares a ref. You can hold any value in it, but most often it’s used to hold a DOM node.
  * `useImperativeHandle` lets you customize the ref exposed by your component. This is rarely used.
* **Effect** - Effects let a component connect to and synchronize with external systems.
  * `useEffect` connects a component to an external system.
  * `useLayoutEffect` fires before the browser repaints the screen. You can measure layout here. (rarely used)
  * `useInsertionEffect` fires before React makes changes to the DOM. Libraries can insert dynamic CSS here. (rarely used)
  * e.g.
    ```javascript
      function ChatRoom({ roomId }) {
    useEffect(() => {
      const connection = createConnection(roomId);
      connection.connect();
      return () => connection.disconnect();
    }, [roomId]);
    // ...
    ```
* **Performance** - skip calculations and unnecessary re-rendering
  * `useMemo` lets you cache the result of an expensive calculation.
  * `useCallback` lets you cache a function definition before passing it down to an optimized component.
  * e.g.
    ```javascript
    function TodoList({ todos, tab, theme }) {
      const visibleTodos = useMemo(() => filterTodos(todos, tab), [todos, tab]);
      // ...
    }
    ```
  * To prioritize rendering, use one of these Hooks:
    * `useTransition` lets you mark a state transition as non-blocking and allow other updates to interrupt it.
    * `useDeferredValue` lets you defer updating a non-critical part of the UI and let other parts update first.
* **Resource**
  * `use` lets you read the value of a resource like a Promise or context.
  * e.g.
    ```javascript
    function MessageComponent({ messagePromise }) {
      const message = use(messagePromise);
      const theme = use(ThemeContext);
      // ...
    }
    ```
