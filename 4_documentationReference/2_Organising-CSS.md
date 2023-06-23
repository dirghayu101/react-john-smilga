Here are different ways of putting CSS in different react components:

1. The basics — inline styles or CSS stylesheets: There are several issues with this approach. For one, the styles are globally accessible. And inline style creates a huge mess.

2. Tailwind CSS or Material UI: Unfortunately, it can also add a lot of clutter to your JSX.

3. CSS-in-JS: CSS-in-JS is another option. There are several popular libraries including styled-components and Emotion. Basically, you use JavaScript to style your components.

4. The best one: CSS Modules: CSS modules are basically CSS files where class names are locally scoped, meaning we can use whatever names we want in the file and not have it accessible to any other component.

First, create the CSS module with whatever name you prefer and append it with .module.css or .module.scss

Then you can import it like this:

```js
import React from "react";
import styles from "./MyComponent.module.css";

const MyComponent = () => {
  return (
    <div>
      <button className={styles.primaryButton}>Click me!</button>
    </div>
  );
};

export default MyComponent;
```

Here are some conventions:

1.  Always use className, avoid IDs or any other attribute for selection: React is all about creating reusable components. Therefore, it makes sense with React to ALWAYS use classNames in your component definition whether or not they will be used once or twice.

2.  BEM: BEM (Block, Element, Modifier) is a popular naming convention for CSS modifiers. It gives your elements’ className context and association.

    Example of BEM:

    ```js
    function Room(props) {
      return (
        <div className="room">
          <div className="room__table">
            <div className="room__paddingContainer">
              // stuff
              <div className="room__bottomLeft">// more stuff</div>
            </div>
          </div>
        </div>
      );
    }
    ```

3.  Create a separate CSS file for each component.
