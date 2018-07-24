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
