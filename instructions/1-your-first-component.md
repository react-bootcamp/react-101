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

Now we want to display the component in the browser. To do that we will use `react-dom` which is a specialized library to render a generic react component inside a DOM environment.

We will use the `render` function of `ReactDOM` to do that

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import { MyComponent } from './MyComponent';

ReactDOM.render(<MyComponent />, document.getElementById('app'));
```

## Pass data to the component

Now that we have a nice component, we want to pass some data inside it. To do that we will use component properties. Properties is an immutable object passed at component instanciation.
To add properties to a component, you just have to declare it like an XML attribute.

Let say we want our component to display a custom message

```javascript
import React, { Component } from 'react';

export class MyComponent extends Component {
  render() {
    const message = this.props.message || 'I am a very useful component';
    return (
      <div className="my-component">
        <h2>{message}</h2>
      </div>
    );
  }
}
```

now to user the property `message` we have to do something like

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import { MyComponent } from './MyComponent';

ReactDOM.render(<MyComponent message="Hello World!" />, document.getElementById('app'));
```

In that case, the displayed message will be `Hello World!`

In React, there is a special property used to create nested components. It's the `children` property

```javascript
import React, { Component } from 'react';

export class MyComponent extends Component {
  render() {
    const message = this.props.message || 'I am a very useful component';
    return (
      <div className="my-component">
        <h2>{message}</h2>
        {this.props.children}
      </div>
    );
  }
}
```

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import { MyComponent } from './MyComponent';

ReactDOM.render(
  <MyComponent message="Hello World!">
    <p>Still a very useful component</p>
  </MyComponent>
  , document.getElementById('app')
);
```

in that case, the displayed message will be `Hello World!` and `this.props.children` will be equal to `<p>Still a very useful component</p>`
