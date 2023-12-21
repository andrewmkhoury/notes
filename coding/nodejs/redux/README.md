# Redux
* https://redux.js.org/

**WARNING**: Many developers complain that redux is complex and it is best to avoid using it unless you absolutely need it or you need to maintain a project that uses it already.

Redux is a predictable state container for JavaScript apps.
* Library for managing application state.
* Used with react-redux library for integrating with react.
* Redux toolkit is the recommended way to write redux logic.

* One way data flow
  * State describes condition of app at point in time and UI renders that.
  * When a change occurs:
    * UI dispatches action
    * Store runs reducers updating state
    * Store notifies the UI
    * UI re-renders based on that


