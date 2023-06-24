<!-- Reference: https://redux.js.org/tutorials/essentials/part-1-overview-concepts -->

Some important Redux terms that you'll need to be familiar with before we continue:

1. Action: An action is a plain JavaScript object that has a type field. You can think of an action as an event that describes something that happened in the application. The type field should be a string that gives this action a descriptive name.

An action object can have other fields with additional information about what happened. By convention, we put that information in a field called payload.

Action object example:

```js
const addTodoAction = {
  type: "todos/todoAdded",
  payload: "Buy milk",
};
```

2. Action Creator: An action creator is a function that creates and returns an action object. We typically use these so we don't have to write the action object by hand every time:

```js
const addTodo = (text) => {
  return {
    type: "todos/todoAdded",
    payload: text,
  };
};
```

3. Reducers: A reducer is a function that receives the current state and an action object, decides how to update the state if necessary, and returns the new state: (state, action) => newState. You can think of a reducer as an event listener which handles events based on the received action (event) type.

Reducers must always follow some specific rules:
a> They should only calculate the new state value based on the state and action arguments
b> They are not allowed to modify the existing state. Instead, they must make immutable updates, by copying the existing state and making changes to the copied values.
c> They must not do any asynchronous logic, calculate random values, or cause other "side effects".

The logic inside reducer functions typically follows the same series of steps:
-> Firstly, it checks to see if the reducer cares about this action. If so, it makes a copy of the state, update the copy with new values, and return it
-> Otherwise, return the existing state unchanged

Example of a reducer:

```js
const initialState = { value: 0 };

function counterReducer(state = initialState, action) {
  // Check to see if the reducer cares about this action
  if (action.type === "counter/increment") {
    // If so, make a copy of `state`
    return {
      ...state,
      // and update the copy with the new value
      value: state.value + 1,
    };
  }
  // otherwise return the existing state unchanged
  return state;
}
```

4. Store: The current Redux application state lives in an object called the store .

The store is created by passing in a reducer, and has a method called getState that returns the current state value:

```js
import { configureStore } from "@reduxjs/toolkit";

const store = configureStore({ reducer: counterReducer });

console.log(store.getState());
// {value: 0}
```
