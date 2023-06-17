Have a look at the following return value from an API:

```js
export const people = [
  { id: 1, name: "bob", nickName: "Stud Muffin" },
  { id: 2, name: "peter" },
  {
    id: 3,
    name: "oliver",
    images: [
      {
        small: {
          url: "https://res.cloudinary.com/diqqf3eq2/image/upload/ar_1:1,bo_5px_solid_rgb:ff0000,c_fill,g_auto,r_max,w_1000/v1595959121/person-1_aufeoq.jpg",
        },
      },
    ],
  },
  { id: 4, name: "david" },
];
```

The problem here in this array of objects is that the object elements are not uniform. Because of this it gets difficult to destructure it.

For example, you might try to destructure it like this:

```js
const img = images[0].small.url;
```

This will give you an error.

For more context this will be the setup:

```js
// The value of people is that API result above.
const List = () => {
  return (
    <div>
      {people.map((person) => {
        console.log(person); //log it to see each person
        return <Person key={person.name} {...person} />;
      })}
    </div>
  );
};

const Person = ({ name, nickname, images }) => {
  const img = images[0].small.url; //This is where you are destructuring it.
  return (
    <div>
      <img src={img} alt={name} style={{ width: "50px" }} />
      <h4>{name} </h4>
      <p>Nickname : {nickName}</p>
    </div>
  );
};
```

Now, the problem is, for some values of person, the nickname will be undefined and for most values images is undefined.

If you try to destructure undefined like this: "images[0].small.url", it will give you an error.

To counter this we used to do it like this:

```js
const img =
  (images && images[0] && images[0].small && images[0].small.url) ||
  someDefaultValue;
```

The above code is verifying in each step if the prior thing exist using ampersand. If it doesn't, it will give it some default value.

But the syntax is lengthy. So, we have this new feature to make it concise called optional chaining.

```js
const img = images?.[0]?.small?.url || avatar;
```

The final program:

```js
import { people } from "../../../data";
import Person from "./Person";
const List = () => {
  return (
    <div>
      {people.map((person) => {
        return <Person key={person.name} {...person} />;
      })}
    </div>
  );
};
export default List;

import React from "react";
import avatar from "../../../assets/default-avatar.svg";
export function Person({ name, nickName = "shakeAndBake", images }) {
  const img = images?.[0]?.small?.url || avatar;

  return (
    <div>
      <img src={img} alt={name} style={{ width: "50px" }} />
      <h4>{name} </h4>
      <p>Nickname : {nickName}</p>
    </div>
  );
}
```

### About Optional Chaining:

Consider an object obj which has a nested structure. Without optional chaining, looking up a deeply-nested sub-property requires validating the references in between, such as:

```js
const nestedProp = obj.first && obj.first.second;
```

The value of obj.first is confirmed to be non-null (and non-undefined) before accessing the value of obj.first.second. This prevents the error that would occur if you accessed obj.first.second directly without testing obj.first.

NOTE: The problem with this pattern: If obj.first is a Falsy value that's not null or undefined, such as 0, it would still short-circuit and make nestedProp become 0, which may not be desirable.

The ?. operator is like the . chaining operator, except that instead of causing an error if a reference is nullish (null or undefined), the expression short-circuits with a return value of undefined. When used with function calls, it returns undefined if the given function does not exist.

```js
const nestedProp = obj.first?.second;
```

By using the ?. operator instead of just ., JavaScript knows to implicitly check to be sure obj.first is not null or undefined before attempting to access obj.first.second. If obj.first is null or undefined, the expression automatically short-circuits, returning undefined.

For more reference: (https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining)
