<!-- Reference:  https://daveceddia.com/what-is-a-reducer/ -->

1. In order to work with Redux, you need to know a few things. One of those things is what a reducer is and what it does.

2. Array.reduce() example:

```js
var letters = ["r", "e", "d", "u", "x"];

// `reduce` takes 2 arguments:
//   - a function to do the reducing (you might say, a "reducer")
//   - an initial value for accumulatedResult
var word = letters.reduce(function (accumulatedResult, arrayItem) {
  return accumulatedResult + arrayItem;
}, ""); // <-- notice this empty string argument: it's the initial value

console.log(word); // => "redux"
```

The reduce function gets called with 2 arguments: the last iteration’s result, and the current array element.

3. Redux Reducer: Similar to how Array.reduce works, Redux is basically a fancy Array.reduce function.

A Redux reducer function has this signature:
(state, action) => newState

As in: it takes the current state, and an action, and returns the newState. Looks a lot like the signature of an Array.reduce reducer, which is this:
(accumulatedValue, nextItem) => nextAccumulatedValue
