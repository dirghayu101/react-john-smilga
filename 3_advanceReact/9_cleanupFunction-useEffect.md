Have a look at this program:

```js
import { useEffect, useState } from "react";

const CleanupFunction = () => {
  const [toggle, setToggle] = useState(false);
  return (
    <div>
      <button className="btn" onClick={() => setToggle(!toggle)}>
        toggle component
      </button>
      {toggle && <RandomComponent />}
    </div>
  );
};
const RandomComponent = () => {
  useEffect(() => {
    console.log("useEffect invoked.");
  }, []);

  return <h1>hello there</h1>;
};
export default CleanupFunction;
```

Every time you toggle the button, useEffect in the RandomComponent will get invoked. This is an observation you have to know about.

Have a look at this version of the above snippet of code:

```js
import { useEffect, useState } from "react";

const CleanupFunction = () => {
  const [toggle, setToggle] = useState(false);
  return (
    <div>
      <button className="btn" onClick={() => setToggle(!toggle)}>
        toggle component
      </button>
      {toggle && <RandomComponent />}
    </div>
  );
};

const RandomComponent = () => {
  useEffect(() => {
    const somFunction = () => {
      // Logic will come here.
    };
    window.addEventListener("scroll", somFunction);
  }, []);

  return <h1>hello there</h1>;
};

export default CleanupFunction;
```

Now this above code will add an event listener for scroll every time you toggle the button.

This can create a lot of problems, as every event listener you are going to add will start a thread and may cause some memory issue in later stage.

To fix this:

```js
const RandomComponent = () => {
  useEffect(() => {
    const someFunction = () => {
      // Logic of someFunction.
    };
    window.addEventListener("scroll", someFunction);
    return () => window.removeEventListener("scroll", someFunction);
  });
};
```

The return here is the cleanup function which will help with the problem.
