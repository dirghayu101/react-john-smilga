These examples are from: https://daveceddia.com/react-redux-immutability-guide/#what-is-immutability

1. Updating an object: When you want to update the top-level properties in the Redux state object, copy the existing state with ...state and then list out the properties you want to change, with their new values.

```js
function reducer(state, action) {
  /*
    State looks like:

    state = {
      clicks: 0,
      count: 0
    }
  */

  return {
    ...state,
    clicks: state.clicks + 1,
    count: state.count - 1,
  };
}
```

2. Updating an object in an object:

```js
function reducer(state, action) {
  /*
    State looks like:

    state = {
      house: {
        name: "Ravenclaw",
        points: 17
      }
    }
  */

  // Two points for Ravenclaw
  return {
    ...state, // copy the state (level 0)
    house: {
      ...state.house, // copy the nested object (level 1)
      points: state.house.points + 2
    }
  }
```

3. Updating a two level object:

```js
function reducer(state, action) {
  /*
    State looks like:

    state = {
      school: {
        name: "Hogwarts",
        house: {
          name: "Ravenclaw",
          points: 17
        }
      }
    }
  */

  // Two points for Ravenclaw
  return {
    ...state, // copy the state (level 0)
    school: {
      ...state.school, // copy level 1
      house: {         // replace state.school.house...
        ...state.school.house, // copy existing house properties
        points: state.school.house.points + 2  // change a property
      }
    }
  }
```

4. Updating an object by key:

```js
function reducer(state, action) {
  /*
    State looks like:

    const state = {
      houses: {
        gryffindor: {
          points: 15
        },
        ravenclaw: {
          points: 18
        },
        hufflepuff: {
          points: 7
        },
        slytherin: {
          points: 5
        }
      }
    }
  */

  // Add 3 points to Ravenclaw,
  // when the name is stored in a variable
  const key = "ravenclaw";
  return {
    ...state, // copy state
    houses: {
      ...state.houses, // copy houses
      [key]: {  // update one specific house (using Computed Property syntax)
        ...state.houses[key],  // copy that specific house's properties
        points: state.houses[key].points + 3   // update its `points` property
      }
    }
  }
```

5. Redux: Prepend an item to an array

The mutable way to do this would be to use Array’s .unshift function to add an item to the front. Array.prototype.unshift mutates the array, though, and that’s not what we want to do.

Here is how you can add an item to the beginning of an array in an immutable way, suitable for Redux:

```js
function reducer(state, action) {
  /*
    State looks like:

    state = [1, 2, 3];
  */

  const newItem = 0;
  return [    // a new array
    newItem,  // add the new item first
    ...state  // then explode the old state at the end
  ];
```

6. Redux: Add an item to an array. The mutable way to do this would be to use Array’s .push function to add an item to the end. That would mutate the array, though.

```js
function reducer(state, action) {
  /*
    State looks like:

    state = [1, 2, 3];
  */

  const newItem = 0;
  return [
    // a new array
    ...state, // explode the old state first
    newItem, // then add the new item at the end
  ];
}
```

Or,

```js
function reducer(state, action) {
  const newItem = 0;
  const newState = state.slice();

  newState.push(newItem);
  return newState;
}
```

7. Redux: Update an item in an array with map. Array’s .map function will return a new array by calling the function you provide, passing in each existing item, and using your return value as the new item’s value.

In other words, if you have an array with N many items and want a new array that still has N items, use .map. You can update/replace one or more items with a single pass through the array.

```js
function reducer(state, action) {
  /*
    State looks like:

    state = [1, 2, "X", 4];
  */

  return state.map((item, index) => {
    // Replace "X" with 3
    // alternatively: you could look for a specific index
    if (item === "X") {
      return 3;
    }

    // Leave every other item unchanged
    return item;
  });
}
```

There are many great examples in this website: https://daveceddia.com/react-redux-immutability-guide/#what-is-immutability
