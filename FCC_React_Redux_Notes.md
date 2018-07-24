# React and Redux Notes

## Getting Started with React Redux
React is a view library that you provide with data, then it renders the view in an efficient, predictable way. Redux is a state management framework that you can use to simplify the management of your application's state. 

In complex app it's generally better to keep the app state in a single location with Redux.

Use the `react-redux` package as it provides a way for you to pass Redux `state` and `dispatch` to your React components as props.

## Extract State Logic to Redux
**Solution**
```javascript
const ADD = 'ADD'

const addMessage = (message) => {
    return{
        message: message,
        type: ADD
    }
}
const defaultState = [];

const messageReducer = (state = defaultState, action) => {
    if(action.type === ADD){
        let newState = [...state, action.message];
        return newState;
    }
    else{
        return state;
    }
};

const store = Redux.createStore(messageReducer);
```

## Use Provider to Connect Redux to React
React Redux provides a small API with two key features: `Provider` and `connect`.

The `Provider` is a wrapper component from React Redux that wraps your React app. This wrapper then allows you to access the Redux `store` and `dispatch` functions throughout your component tree. 

`Provider` takes two props, the Redux store and the child components of your app.

**Solution**
```javascript
const Provider = ReactRedux.Provider;

class AppWrapper extends React.Component {
  // render the Provider here
  render(){
      return(
        <Provider store={store}>
            <DisplayMessages/>
        </Provider>
      )
  }
  // change code above this line
};
```

## Map State to Props
`mapStateToProps()` and `mapDispatchToProps()` in these functions, you declare what pieces of state you want to have access to and which action creators you need to be able to dispatch. 

You can use these functions to map `state` and `dispatch` to the `props` of one of your React components.

Behind the scenes, React Redux uses the `store.subscribe()` method to implement `mapStateToProps()`.

const state = [];

**Solution**
```javascript
// change code below this line
function mapStateToProps(state){
  return{
    messages: state
  }
}
```

## Map Dispatch to Props
The `mapDispatchToProps()` function is used to provide specific action creators to your React components so they can dispatch actions against the Redux store.

It returns an object that maps dispatch actions to property names, which become component `props`. 

Behind the scenes, React Redux is using Redux's `store.dispatch()` to conduct these dispatches with `mapDispatchToProps()`.

**Solution**
```javascript
const addMessage = (message) => {
  return {
    type: 'ADD',
    message: message
  }
};

// change code below this line
function mapDispatchToProps(dispatch){
    return{
        submitNewMessage: function(msg) {
            dispatch(addMessage(msg));
        }
    }
}
```

## Connect Redux to React
`connect` method from React Redux takes two optional arguments, `mapStateToProps()` and `mapDispatchToProps()`.

To use this method, pass in the functions as arguments, and immediately call the result with your component. 
```javascript
const connect = ReactRedux.connect;
connect(mapStateToProps, mapDispatchToProps)(MyComponent)
```

