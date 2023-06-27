Normal react application data flow:

1. In a normal react application there is one-way data flow.
2. State describes the condition of the app at a specific point in time
3. The UI is rendered based on that state
4. When something happens (such as a user clicking a button), the state is updated based on what occurred
5. The UI re-renders based on the new state

Redux application data flow:

1. Initial Setup:
   a> A Redux store is created using a root reducer function
   b> The store calls the root reducer once, and saves the return value as its initial state
   c> When the UI is first rendered, UI components access the current state of the Redux store, and use that data to decide what to render. They also subscribe to any future store updates so they can know if the state has changed.

2. Updates:
   a> Something happens in the app, such as a user clicking a button
   b> The app code dispatches an action to the Redux store, like dispatch({type: 'counter/increment'})
   c> The store runs the reducer function again with the previous state and the current action, and saves the return value as the new state
   d> The store notifies all parts of the UI that are subscribed that the store has been updated
   e> Each UI component that needs data from the store checks to see if the parts of the state they need have changed.
   f> Each component that sees its data has changed forces a re-render with the new data, so it can update what's shown on the screen
