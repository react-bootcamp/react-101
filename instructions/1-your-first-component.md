# Your first React component

Now that your server is running with a blank React app, we can start to work

## What is a React component

There are several ways to define a React component. Each React component will be defined as a `class` that you will be able to instanciate in your views.

**WARNING**: the first letter of the name of a React component should always be Uppercase.

## `React.createClass`

The first way to define a React component is the ancient way using `React.createClass`

```javascript
import React from 'react';

export const MyComponent = React.createClass({
  render() {
    return (
      <div className="my-component">
        <h2>I am a very useful component</h2>
      </div>
    );
  }
});
```

as you can see, a React component is something really simple. Its only requirement is to have a `render` function that will return the `view` of the component.

And now, i'm pretty sure that you are asking yourself, WTF is `<div>...</div>` inside my JS code ?
Don't panic, it's just some JSX.

## JSX

[JSX](https://facebook.github.io/jsx/) is a JavaScript syntax extension that looks similar to XML. Actually, your javascript code will be pre-processed before landing in the browser and will be transformed into regular javascript. If you dont like JSX, React doesn't force you to use it, you can just write your component this way

```javascript
import React from 'react';

// can be replace with
// import React, { createElement: e } from 'react';
const e = React.createElement;

export const MyComponent = React.createClass({
  render() {
    return (
      e('div', { className: 'my-component' },
        e('h2', null, 'I am a very useful component')
      )
    );
  }
});
```

## `React.Component`

The second way to define a component is to use ES6 classes

```javascript
import React, { Component } from 'react';

export class MyComponent extends Component {
  render() {
    return (
      <div className="my-component">
        <h2>I am a very useful component</h2>
      </div>
    );
  }
}
```

## Functional component

The last way to define a component is to use pure functions. It is quite useful to write small stateless components

```javascript
import React, { Component } from 'react';

export const MyComponent = () => (
  <div className="my-component">
    <h2>I am a very useful component</h2>
  </div>
);
```

## Mounting a component into the DOM
