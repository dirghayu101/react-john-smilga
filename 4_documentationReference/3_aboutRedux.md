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

6.

References:

1. https://changelog.com/posts/when-and-when-not-to-reach-for-redux
2. https://daveceddia.com/javascript-references/
3.
