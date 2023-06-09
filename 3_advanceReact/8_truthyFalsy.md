In JavaScript, a value is considered "truthy" if it is evaluated to true when used in a boolean context. A value is considered "falsy" if it is evaluated to false when used in a boolean context.

We cannot use if statement in JSX return, so we use this truthy and falsy thing instead.

Here is a list of values that are considered falsy in JavaScript:

false
0 (zero)
"" (empty string)
null
undefined
NaN (Not a Number)

All other values, including objects and arrays, are considered truthy.

Truthy and Falsy values can help you write concise code.

Ternary operation:

```js
<div>{isLoggedIn ? <AdminPanel /> : <LoginForm />}</div>
```

When you don’t need the else branch, you can also use a shorter logical && syntax:

```js
<div>{isLoggedIn && <AdminPanel />}</div>
```

One way of doing it is by using short circuit evaluation.

In JavaScript, short-circuit evaluation is a technique that allows you to use logical operators (such as && and ||) to perform conditional evaluations in a concise way.

The && operator (logical AND) returns the first operand if it is "falsy", or the second operand if the first operand is "truthy".

Example:

1. console.log(x && y); // Output: 0 (the first operand is falsy, so it is returned)
2. console.log(y && x); // Output: 0 (the second operand is falsy, so it is returned)

The || operator (logical OR) returns the first operand if it is "truthy", or the second operand if the first operand is "falsy".

Example:

1. console.log(x || y); // Output: 1 (the first operand is falsy, so the second operand is returned)
2. console.log(y || x); // Output: 1 (the first operand is truthy, so it is returned)

Short-circuit evaluation can be useful in cases where you want to perform a certain action only if a certain condition is met, or you want to return a default value if a certain condition is not met.

Example:

```js
function displayName(name) {
  return name || "Anonymous";
}

console.log(displayName("Pizza")); // Output: "Pizza"
console.log(displayName()); // Output: "Anonymous"
```

/**\*\***\*\*\*\***\*\***\*\***\*\***\*\*\*\***\*\***\*\***\*\***\*\*\*\***\*\***\*\***\*\***\*\*\*\***\*\***/

Have a look at this program:

```js
import { useState } from "react";

const ShortCircuitOverview = () => {
  // falsy
  const [text, setText] = useState("");
  // truthy
  const [name, setName] = useState("susan");

  const codeExample = text || "hello world";

  // can't use if statements
  return (
    <div>
      {/* {if(someCondition){"won't work"}} */}

      <h4>Falsy OR : {text || "hello world"}</h4>
      <h4>Falsy AND {text && "hello world"}</h4>
      <h4>Truthy OR {name || "hello world"}</h4>
      <h4>Truthy AND {name && "hello world"}</h4>
      {codeExample}
    </div>
  );
};

export default ShortCircuitOverview;
```

/**\*\***\*\*\*\***\*\***\*\***\*\***\*\*\*\***\*\***\*\***\*\***\*\*\*\***\*\***\*\***\*\***\*\*\*\***\*\***/

Go through the below code. Another example starts here:

```js
import { useState } from "react";

const ShortCircuitExamples = () => {
  // falsy
  const [text, setText] = useState("");
  // truthy
  const [name, setName] = useState("susan");
  const [user, setUser] = useState({ name: "john" });
  const [isEditing, setIsEditing] = useState(false);

  return (
    <div>
      {/* content inside element */}
      <h2>{text || "default value"}</h2>
      {/* toggle element */}
      {text && (
        <div>
          <h2> whatever return</h2>
          <h2>{name}</h2>
        </div>
      )}
      {/* more info below */}
      {!text && <h4>also works</h4>}
      {/* toggle component */}
      {user && <SomeComponent name={user.name} />}
      <h2 style={{ margin: "1rem 0" }}>Ternary Operator</h2>
      {/* inside element */}
      <button className="btn">{isEditing ? "edit" : "add"}</button>
      {/* toggle elements/components */}
      {user ? (
        <div>
          <h4>hello there user {user.name}</h4>
        </div>
      ) : (
        <div>
          <h2>please login</h2>
        </div>
      )}
    </div>
  );
};

const SomeComponent = ({ name }) => {
  return (
    <div>
      <h4>hello there, {name}</h4>
      <button className="btn">log out</button>
    </div>
  );
};
export default ShortCircuitExamples;
```
