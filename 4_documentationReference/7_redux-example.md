We are going to look at a react-redux application.

The application structure will looks like this:
/src
    index.js: the starting point for the app
    App.js: the top-level React component
/app
    store.js: creates the Redux store instance
/features
    /counter
        Counter.js: a React component that shows the UI for the counter feature
        counterSlice.js: the Redux logic for the counter feature


The /features/counter/counterSlice.js file with redux logic:
```js
import { createSlice } from "@reduxjs/toolkit";

export const counterSlice = createSlice({
  name: "counter",
  initialState: {
    value: 0,
  },
  reducers: {
    increment: (state) => {
      // Redux Toolkit allows us to write "mutating" logic in reducers. It
      // doesn't actually mutate the state because it uses the immer library,
      // which detects changes to a "draft state" and produces a brand new
      // immutable state based off those changes
      state.value += 1;
    },
    decrement: (state) => {
      state.value -= 1;
    },
    incrementByAmount: (state, action) => {
      state.value += action.payload;
    },
  },
});

export const { increment, decrement, incrementByAmount } = counterSlice.actions;

// The function below is called a thunk and allows us to perform async logic. It
// can be dispatched like a regular action: `dispatch(incrementAsync(10))`. This
// will call the thunk with the `dispatch` function as the first argument. Async
// code can then be executed and other actions can be dispatched
export const incrementAsync = (amount) => (dispatch) => {
  setTimeout(() => {
    dispatch(incrementByAmount(amount));
  }, 1000);
};

// The function below is called a selector and allows us to select a value from
// the state. Selectors can also be defined inline where they're used instead of
// in the slice file. For example: `useSelector((state) => state.counter.value)`
export const selectCount = (state) => state.counter.value;

export default counterSlice.reducer;
```


# Explanation of /features/counter/counterSlice.js file:
-> Redux Toolkit has a function called createSlice, which takes care of the work of generating action type strings, action creator functions, and action objects. All you have to do is define a name for this slice, write an object that has some reducer functions in it, and it generates the corresponding action code automatically. 
-> The string from the name option is used as the first part of each action type, and the key name of each reducer function is used as the second part. So, the "counter" name + the "increment" reducer function generated an action type of {type: "counter/increment"}. 


The app/store.js will look like this:
```js
import { configureStore } from "@reduxjs/toolkit";
import counterReducer from "../features/counter/counterSlice";

export default configureStore({
  reducer: {
    counter: counterReducer,
  },
});
```

# Explanation of app/store.js:
-> The Redux store is created using the configureStore function from Redux Toolkit. configureStore requires that we pass in a reducer argument.
-> When we pass in an object like {counter: counterReducer}, that says that we want to have a state.counter section of our Redux state object, and that we want the counterReducer function to be in charge of deciding if and how to update the state.counter section whenever an action is dispatched.
-> createSlice uses a library called Immer inside. Immer uses a special JS tool called a Proxy to wrap the data you provide, and lets you write code that "mutates" that wrapped data.  
-> Immer tracks all the changes you've tried to make, and then uses that list of changes to return a safely immutably updated value, as if you'd written all the immutable update logic by hand.



# Redux Slice: 
-> A "slice" is a collection of Redux reducer logic and actions for a single feature in your app, typically defined together in a single file. The name comes from splitting up the root Redux state object into multiple "slices" of state.
-> Look at this configureStore export:
```js
    export default configureStore({
    reducer: {
        users: usersReducer,
        posts: postsReducer,
        comments: commentsReducer
    }
    })
```
-> In the above example, state.users, state.posts, and state.comments are each a separate "slice" of the Redux state. Since usersReducer is responsible for updating the state.users slice, we refer to it as a "slice reducer" function.


The /features/counter/Counter.js component file:
```js
import React, { useState } from 'react'
import { useSelector, useDispatch } from 'react-redux'
import {
  decrement,
  increment,
  incrementByAmount,
  incrementAsync,
  selectCount
} from './counterSlice'
import styles from './Counter.module.css'

export function Counter() {
  const count = useSelector(selectCount)
  const dispatch = useDispatch()
  const [incrementAmount, setIncrementAmount] = useState('2')

  return (
    <div>
      <div className={styles.row}>
        <button
          className={styles.button}
          aria-label="Increment value"
          onClick={() => dispatch(increment())}
        >
          +
        </button>
        <span className={styles.value}>{count}</span>
        <button
          className={styles.button}
          aria-label="Decrement value"
          onClick={() => dispatch(decrement())}
        >
          -
        </button>
      </div>
      {/* omit additional rendering output here */}
    </div>
  )
}
```