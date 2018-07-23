# FCC Redux Notes

## Redux: Create a Redux Store

Redux is a state management framework that can be used with a number of different web technologies, including React.

Redux **store** is the single source of truth when it comes to application state. It is single state object that's responsible 
for the entire state of your application.

Solution:

const reducer = (state = 5) => {
  return state;
}

// Redux methods are available from a Redux object
// For example: Redux.createStore()
// Define the store here:
let store = Redux.createStore(reducer);
