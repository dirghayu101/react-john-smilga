Some points:

1. Redux is a very generic state management tool that can be used for a broad array of use cases.
   -> Caching state from a server
   -> UI state
   -> other complex data management on the client

2. It’s probably not going to be the best or most efficient tool at any of those use cases. Other tools like React Query or Apollo are much more specialized for this specific case of data fetching.
   So you can do many things with Redux. It might not be quite the best at all of them, but you can do lots of different things.

3. One important property of javascript: There are the primitive types like string, number, boolean (and also symbol, undefined, and null). These ones are immutable. a.k.a. read-only, can’t be changed.
   Said another way, when the value inside a box is a string/number/boolean/symbol/undefined/null, you can’t change the value. You can only create new boxes.

The other category is the object type. This encompasses objects, arrays, functions, and other data structures like Map and Set. They are all objects. The big difference from primitive types is that objects are mutable! You can change the value in the box.

4. If you pass a primitive value into a function, the original variable you passed in is guaranteed to be left alone. The function can’t modify what’s inside it. You can rest assured that the variable will always be the same after calling a function – any function.

But with objects and arrays (and the other object types), you don’t have that assurance. If you pass an object into a function, that function could change your object. If you pass an array, the function could add new items to it, or empty it out entirely.

So this is one reason why a lot of people in the JS community try to write code in an immutable way: it’s easier to figure out what the code does when you’re sure your variables won’t change unexpectedly. If every function is written to be immutable by convention, you never need to wonder what will happen.

A function that doesn’t change its arguments, or anything outside of itself, is called a pure function. If it needs to change something in one of its arguments, it’ll do that by returning a new value instead. This is more flexible, because it means the calling code gets to decide what to do with that new value. Immutability is predictable.

5. In React’s case, it’s important to never mutate state or props. Whether a component is a function or a class doesn’t matter for this rule. If you’re about to write code like this.state.something = ... or this.props.something = ..., take a step back and try to come up with a better way.

To modify state, always use this.setState.

6. By default, React components (both the function type and the class type, if it extends React.Component) will re-render whenever their parent re-renders, or whenever you change their state with setState.

An easy way to optimize a React component for performance is to make it a class, and make it extend React.PureComponent instead of React.Component. This way, the component will only re-render if its state is changed or if its props have changed. It will no longer mindlessly re-render every single time its parent re-renders; it will ONLY re-render if one of its props has changed since the last render.

Here’s where immutability comes in: if you’re passing props into a PureComponent, you have to make sure that those props are updated in an immutable way. That means, if they’re objects or arrays, you’ve gotta replace the entire value with a new (modified) object or array. Just like with Bob – kill it off and replace it with a clone.

7. When you compare two objects or arrays with the === operator, JavaScript is actually comparing the addresses they point to – a.k.a. their references. JS does not even peek into the object. It only compares the references. That’s what “referential equality” means.

8. Does const Prevent Changes?
   The short answer is: no. Neither let nor const nor var will prevent you from changing the internals of an object. All three ways of declaring a variable allow you to mutate its internals.
   “But it’s called const! Isn’t that supposed to be constant?”
   Well, sorta. const will only prevent you from reassigning the reference. It doesn’t stop you from changing the object.

9. How is all this talks about pure-function, mutability and immutability relevant in redux?
   It is relevant because redux requires that its reducers be pure functions. This means you can’t modify the state directly – you have to create a new state based on the old one.

10. It's quite tricky to copy a mutable object in javascript. Look at this example:

    ```js
    // Internal properties are left alone:
    let company = {
      name: "Foo Corp",
      people: [{ name: "Joe" }, { name: "Alice" }],
    };
    let newCompany = { ...company };
    newCompany === company; // => false! not the same object
    newCompany.people === company.people; // => true!
    ```

11.

References:

1. https://changelog.com/posts/when-and-when-not-to-reach-for-redux
2. https://daveceddia.com/javascript-references/
3. https://daveceddia.com/react-redux-immutability-guide/#what-is-immutability -> Best.
4.
