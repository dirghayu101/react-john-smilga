-> So using the concept of Dynamic Object Key, you can create this very efficient form with just one useState hook.

-> Every useState you use will increase the number of times a form is going to re-render, so this is a really good approach.

-> Go through the code below:

```js
import { useState } from "react";
const MultipleInputs = () => {
  const [user, setUser] = useState({
    name: "",
    email: "",
    password: "",
  });

  const handleChange = (e) => {
    // setUser({ [e.target.name]: e.target.value });
    setUser({ ...user, [e.target.name]: e.target.value });
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log(user);
  };
  return (
    <div>
      <form className="form" onSubmit={handleSubmit}>
        <h4>Multiple Inputs</h4>
        {/* name */}
        <div className="form-row">
          <label htmlFor="name" className="form-label">
            name
          </label>
          <input
            type="text"
            className="form-input"
            id="name"
            name="name"
            value={user.name}
            onChange={handleChange}
          />
        </div>
        {/* email */}
        <div className="form-row">
          <label htmlFor="email" className="form-label">
            Email
          </label>
          <input
            type="email"
            className="form-input"
            id="email"
            name="email"
            value={user.email}
            onChange={handleChange}
          />
        </div>
        {/* email */}
        <div className="form-row">
          <label htmlFor="password" className="form-label">
            Password
          </label>
          <input
            type="password"
            className="form-input"
            id="password"
            name="password"
            value={user.password}
            onChange={handleChange}
          />
        </div>

        <button type="submit" className="btn btn-block">
          submit
        </button>
      </form>
    </div>
  );
};
export default MultipleInputs;
```

NOTE: When I replace the handleChange update method: "setUser({ ...user, [e.target.name]: e.target.value });"
with this: setUser({ [e.target.name]: e.target.value });
It overrides the entire object and creates a new object with just one key value pair. Spread operation retains the default values and override the only new entry value.

### About Dynamic Object Key:

In Javascript, creating and adding values to an object with a static key can be done as below.

```js
const person = { name: "Joshi", age: 30 };
//Accessing Object
person.name; //Joshi
person.age; //30
```

This is not valid:

```js
//If firstName has valid value, Object should have 'firstName' as key, else 'name'
const hasFirstName = true;
let nameKey = hasFirstName ? "firstName" : "name";
const person = { nameKey: "Joshi", age: 21 };

person; //{nameKey: "Joshi", age: 21}
```

If you add a variable name to the Object key, It will take the variable name as the key, not the variable value.

To have dynamic value as a key, use [] to add value to the object as below.

Example:

```js
const hasFirstName = true;
let nameKey = hasFirstName ? "firstName" : "name";
let person = {};
person[nameKey] = "Joshi";
person["age"] = 21;
person; //{firstName: "Joshi", age: 21}
```
