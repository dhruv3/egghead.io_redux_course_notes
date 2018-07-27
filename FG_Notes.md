# F G Notes

React parent child heirarchy not always possible. You cannot have parent-child setup for every part of your application. 
State management tough. So Redux. 

Redux is state-management lib. Works on flux architecture. No relation with React.

3 simple concepts:

1. **Application level state**: it will be object with entire data. You decide keys. Scholarship, login, user-profile. Called **STORE**.

2. If i want to change state i’ll dispatch Action to redux. **Action** is an obj. Redux makes changes to BIG object. {type: payload}.

3. State change happens through **reducer**. Reducer is a Pure function that uses action, action type, prevstate and to give nextstate.

React and Redux **connection**

Reducer: its a function. Object immutability. Object.assign. Redux init.

**Root** reducer

Provider is a connection between React and Redux. Store which has root-reducer. Store as a HOC wraps entire app.

HOC used so as to communicate. 

Connect React and Redux using connect. React comp calls dispatch. Reducer gets action. Store updated and reaches component

mapStateToProps-> key updated-> re-render component

Action flows through all reducers

Multiple reducer so as to modular

Order is important

MIDDLEWARE

Redux promise lib

For async actions. Promise wait completion then action dispatch. 

# Spapas Tutorial

[Link](https://spapas.github.io/2016/03/02/react-redux-tutorial/)

The general idea/flow is:

* Something (let’s call it event) happens (i.e a user clicks a button, a timeout is fired, an ajax request responds)
* An action describing that event is created by its the corresponding action creator and dispatched (i.e passed to the reducer along with the current state) through the store
* The dispach calls the reducer with the current state object and the action as parameters
* The reducer checks the type of the action and, depending on the action type and any other properties this action has, creates a new state object
* The store applies the new state to all components

React **context** feature that allows you to “pass data through the component tree without having to pass the props down manually at every level”.

The `mapStateToProps` is a function that will be called whenever the store’s state changes and should return an object whose attributes will be passed to the connected component as properties.

The `mapDispatchToProps` as we use it, once again returns an object whose attributes will be passed to the connected component and will dispatch actions when called.
