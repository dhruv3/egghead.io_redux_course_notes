# FCC Redux Notes

## Create a Redux Store

Redux is a state management framework that can be used with a number of different web technologies, including React.

Redux `store` is the single source of truth when it comes to application state. It is single state object that's responsible 
for the entire state of your application.

**Solution:**
```javascript
const reducer = (state = 5) => {
  return state;
}

// Redux methods are available from a Redux object
// For example: Redux.createStore()
// Define the store here:
let store = Redux.createStore(reducer);
```

## Get State from the Redux Store

You can retrieve the current `state` held in the Redux store object with the `getState()` method.
**Solution:**
```javascript
const store = Redux.createStore(
  (state = 5) => state
);
let currentState = store.getState();
```

## Define a Redux Action

In Redux, all state updates are triggered by dispatching actions. 

An action is simply a JavaScript object that contains information about an action event that has occurred. Actions must carry a type property that specifies the `type`of action that occurred.

The Redux store receives these action objects, then updates its state accordingly. Sometimes a Redux action also carries some data. 

**Solution:**
```javascript
let action = {
  type: 'LOGIN'
}
```

## Define an Action Creator

An action creator is simply a JavaScript function that returns an action. In other words, action creators create objects that represent action events.

**Solution:**
```javascript
const action = {
  type: 'LOGIN'
}
// Define an action creator here:
function actionCreator(){
    return action;
}
```

## Dispatch an Action Event

`dispatch` method is what you use to dispatch actions to the Redux store. 

Calling `store.dispatch()` and passing the value returned from an action creator sends an action back to the store.

**Solution:**
```javascript
const store = Redux.createStore(
  (state = {login: false}) => state
);

const loginAction = () => {
  return {
    type: 'LOGIN'
  }
};

// Dispatch the action here:
store.dispatch(loginAction())
```

## Handle an Action in the Store
Reducers in Redux are responsible for the state modifications that take place in response to actions. 

A `reducer` takes `state` and `action` as arguments, and it always returns a new `state`.

The reducer is simply a pure function that takes state and action, then returns new state.

Redux `state` are IMMUTABLE. `reducer` function must always return a new copy of `state` and never modify state directly.

**Solution**
```javascript
const defaultState = {
  login: false
};

const reducer = (state = defaultState, action) => {
  // change code below this line
  let newState = Object.assign({}, state);
  if(action.type === 'LOGIN'){
    newState['login'] = true;
    return newState;
  }
  else{
    return state;
  }
  // change code above this line
};

const store = Redux.createStore(reducer);

const loginAction = () => {
  return {
    type: 'LOGIN'
  }
};
```

## Use a Switch Statement to Handle Multiple Actions

**Solution**
```javascript
const defaultState = {
  authenticated: false
};

const authReducer = (state = defaultState, action) => {
  // change code below this line
  switch(action.type){
    case 'LOGIN':
      return {authenticated: true};
    case 'LOGOUT':
      return {authenticated: false};
    default:
      return state;
  }
  // change code above this line
};

const store = Redux.createStore(authReducer);

const loginUser = () => {
  return {
    type: 'LOGIN'
  }
};

const logoutUser = () => {
  return {
    type: 'LOGOUT'
  }
};
```

## Use const for Action Types
A common practice when working with Redux is to assign action types as read-only constants, then reference these constants wherever they are used.

## Register a Store Listener
`store.subscribe()` allows you to subscribe listener functions to the store, which are called whenever an action is dispatched against the store.

**Solution**
```javascript
const ADD = 'ADD';

const reducer = (state = 0, action) => {
  switch(action.type) {
    case ADD:
      return state + 1;
    default:
      return state;
  }
};

const store = Redux.createStore(reducer);

// global count variable:
let count = 0;
function cb(){
  count += 1;
}
store.subscribe(cb);
// change code below this line

// change code above this line

store.dispatch({type: ADD});
console.log(count);
store.dispatch({type: ADD});
console.log(count);
```

## Combine Multiple Reducers
Redux provides reducer composition using which you can define multiple reducers to handle different pieces of your application's state, then compose these reducers together into one root reducer. 

The root reducer is then passed into the Redux `createStore()` method.

We use `combineReducers()` method to combine multiple reducers together. This method accepts an object as an argument in which you define properties which associate keys to specific reducer functions.

**Solution**
```javascript
const rootReducer = Redux.combineReducers({
  count: counterReducer,
  auth: authReducer
})
```
## Send Action Data to the Store
**Solution**
```javascript
const ADD_NOTE = 'ADD_NOTE';

const notesReducer = (state = 'Initial State', action) => {
  switch(action.type) {
    // change code below this line
    case "ADD_NOTE":
      return action.text;
    // change code above this line
    default:
      return state;
  }
};

const addNoteText = (note) => {
  // change code below this line
  return{
    type: 'ADD_NOTE',
    text: note
  }
  // change code above this line
};

const store = Redux.createStore(notesReducer);

console.log(store.getState());
store.dispatch(addNoteText('Hello!'));
console.log(store.getState());
```

## Use Middleware to Handle Asynchronous Actions
Redux Thunk middleware for asynchronous handling.
```javascript
const store = Redux.createStore(
  asyncDataReducer,
  Redux.applyMiddleware(ReduxThunk.default)
);
```
It's common to dispatch an action before initiating any asynchronous behavior so that your application state knows that some data is being requested (this state could display a loading icon, for instance). Then, once you receive the data, you dispatch another action which carries the data as a payload along with information that the action is completed.
```javascript
const handleAsync = () => {
  return function(dispatch) {
    // dispatch request action here
    console.log("store");
    store.dispatch(requestingData());
    setTimeout(function() {
      let data = {
        users: ['Jeff', 'William', 'Alice']
      }
      // dispatch received data action here
      store.dispatch(receivedData(data));
    }, 2500);
  }
};
```
## Write a Counter with Redux
**Solution**
```javascript
const INCREMENT = 'INCREMENT'; // define a constant for increment action types
const DECREMENT = 'DECREMENT'; // define a constant for decrement action types

const counterReducer = (state = 0, action) => {
  switch(action.type) {
    case INCREMENT:
      return state + 1;
    case DECREMENT:
      return state - 1;
    default:
      return state;
  }
};; // define the counter reducer which will increment or decrement the state based on the action it receives

const incAction = () => {
  return {
    type: INCREMENT
  }
}; // define an action creator for incrementing

const decAction = () => {
  return {
    type: DECREMENT
  }
}; // define an action creator for decrementing

const store = Redux.createStore(counterReducer); // define the Redux store here, passing in your reducers
```
## Never Mutate State
How to deal with state and immutability:

**Way 1**
```javascript
let newTodo = Object.assign([], state);
newTodo.push(action.todo);
```
**Way 2**
```javascript
let newState = [...state, action.todo];
```
