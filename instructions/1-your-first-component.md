# Your first React component

Now that your server is running with a blank React app, we can start to work

## What is a React component

There are several ways to define a React component. Each React component will be defined as a `class` that you will be able to instanciate in your views.

**WARNING**: the first letter of the name of a React component should always be **Uppercase**.

## `React.createClass`

The first way to define a React component is the "ancient" way using `React.createClass`, **we will not use** `React.createClass` in this workshop.

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

It's the new official way to define stateful components, therefore, **it will be used everywhere in the workshop**.

## Functional component

The last way to define a component is to use pure functions. It is quite useful to write small stateless components

```javascript
import React from 'react';

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

ReactDOM.render(<MyComponent />, document.getElementById('root'));
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

//                          the props is passed here
//                                    |||
//                           vvvvvvvvvvvvvvvvvvvvvv  
ReactDOM.render(<MyComponent message="Hello World!" />, document.getElementById('root'));
```

In that case, the displayed message will be `Hello World!`

You can provide default values for `props` using static property `defaultProps`

```javascript
import React, { Component } from 'react';

export class MyComponent extends Component {

  static defaultProps = {
    message: 'I am a very useful component';
  };

  render() {
    return (
      <div className="my-component">
        <h2>{this.props.message}</h2>
      </div>
    );
  }
}
```

You can provide some validation for the `props` of a component using `React.PropTypes` to have error message in developement. it's quite useful when you provide components to other dev teams.

```javascript
import React, { Component } from 'react';
import PropTypes from 'prop-types';

export class MyComponent extends Component {

  static propTypes = {
    message: PropTypes.string
  };

  static defaultProps = {
    message: 'I am a very useful component'
  };

  render() {
    return (
      <div className="my-component">
        <h2>{this.props.message}</h2>
      </div>
    );
  }
});
```

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
  , document.getElementById('root')
);
```

in that case, the displayed message will be `Hello World!` and `this.props.children` will be equal to `<p>Still a very useful component</p>`

## Store data inside the component using the component state

If components `props` are not enought for your need, you can use the component `state`. The state is specific value for each component instance. Each time the value of the state is changed using `this.setState(...)`, this will trigger a full redraw of the component. Let's write a counter component

```javascript
import React, { Component } from 'react';

export class Counter extends Component {

  state = { // if you don't define an initial state, your state will be null
    count: 0
  };

  incrementCounter = () => {
    this.setState({ count: this.state.count + 1 }); // trigger a component redraw
  };

  render() {
    return (
      <div>
        <h2>Count: {this.state.count}</h2>
        <button type="button" onClick={() => this.incrementCounter()}>increment</button>
      </div>
    );
  }
}
```

you can't implement the counter as a functional component because functional component don't have a state.

## Store data inside the component using the component instance

If your when to store something technical in a component instance without triggering a redraw of the component, you can just store whatever you want on `this`

```javascript
import React, { Component } from 'react';

export class Clock extends Component {

  state = { // if you don't define an initial state, your state will be null
    time: Date.now()
  };

  update = () => {
    this.setState({ time: Date.now() });
  };

  componentDidMount() { // will be called when component is mounted in the DOM
    this.interval = setInterval(this.update, 1000); // here we store the interval id on the component instance
  }

  componentWillUnmount() { // will be called when component is removed from the DOM
    clearInterval(this.interval);
  }

  render() {
    return (
      <div>
        <h2>Count: {this.state.count}</h2>
        <button type="button" onClick={this.incrementCounter}>increment</button>
      </div>
    );
  }
}
```

# It's time to write a Wine component

Let's write a nice component that will display details of a wine. This wine will be provided as a property.

First let's just display it's name

```javascript
import React, { Component } from 'react';
import PropTypes from 'prop-types';

export class Wine extends Component {

  static propTypes = {
    wine: PropTypes.shape({
      name: PropTypes.string
    })
  };

  static defaultProps = {
    wine: {
      name: 'Some Wine'
    }
  };

  render() {
    return (
      <div className="card horizontal">   
        <div className="card-stacked">
          <div className="card-content">
            <h3>{this.props.wine.name}</h3>
          </div>
        </div>
      </div>
    );
  }
}
```

to mount it just write something like

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import { Wine } from './Wine';

const wine = { name: 'Château Chevrol Bel Air' };

ReactDOM.render(
  <Wine wine={wine}/>, document.getElementById('root')
);
```

now it's up to you !!! let say a wine is an object like that

```javascript
{
  "id": "chevrol-bel-air",
  "name": "Château Chevrol Bel Air",
  "type": "Red",
  "appellation": {
    "name": "Lalande-de-Pomerol",
    "region": "Bordeaux"
  },
  "grapes": [
    "Cabernet Sauvignon",
    "Merlot",
    "Cabernet Franc"
  ]
}
```

and we want the component to look like the following HTML snippet

```html
<div class="card horizontal">
  <div class="card-stacked">
    <div class="card-content">
      <h3>Wine name</h3>
      <br/>
      <p><b>Appellation:</b> Wine appellation name</p>
      <p><b>Region:</b> Wine appellation region</p>
      <p><b>Color:</b> Wine type</p>
      <p><b>Grapes:</b> Wine grape 1, Wine grape 2</p>
    </div>
  </div>
</div>
```

# Adding likes

Now we are going to make the `<Wine />` component stateful. We are going to add a `like` button to count how many likes the wine gets

Let say the `<Wine />` component should now look like

```html
<div class="card horizontal">
  <div class="card-stacked">
    <div class="card-content">
      <h3>Wine name</h3>
      <br/>
      <p><b>Appellation:</b> Wine appellation name</p>
      <p><b>Region:</b> Wine appellation region</p>
      <p><b>Color:</b> Wine type</p>
      <p><b>Grapes:</b> Wine grape 1, Wine grape 2</p>
    </div>
    <div class="card-action">
      <a class="waves-effect waves-teal btn-flat">
        <span>Like <i className="material-icons left">thumb_up</i> (42)</span>
      </a>
   </div>
  </div>
</div>
```

to achieve that, you will create a new component called `<LikeButton />` with the following contract

```javascript
import React, { Component } from 'react';
import PropTypes from 'prop-types';

export class LikeButton extends Component {

  static propTypes = {
    startCounterAt: PropTypes.number
  };

  ...
}
```

the `<LikeButton />` component will have a state to hold the number of likes for the button and a click listener to increment the like counter.

# What's next

Now you're ready to write the Wine application. Go to the [next step](./2-the-wine-app.md) to start writing it.
