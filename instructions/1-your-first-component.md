# Your first React component

Now that your server is running with a blank React app, we can start to work

## What is a React component

There are several ways to define a React component. Each React component will be defined as a `class` that you will be able to instanciate in your views.

The first way to define a React component is the ancient way using `React.createClass`

## `React.createClass`

```javascript
import React from 'react';

export const MyComponent = React.createClass({
  render() {
    return (
      <div>
        <h2>I am a very useful component</h2>
      </div>
    );
  }
});
```

as you can see, a React component is something really simple. Its only requirement is to have a `render` function that will return the `view` of the component.

And now, i'm pretty sure that you are asking your

## JSX
