# Classic patterns with React

## Component styling

There are several way to style a component. It's quite a challenge to encapsulate style for a component but also allow customization.

### Classic styling

You can style your components using the classic `class` attribute. In React, it's translated to the `className` property.

```jsx
<div className="a-class">...</div>
```

You can use multiple classes

```jsx
<div className="a-class another-class">...</div>
```

You can use some tricks to add classes conditionaly

```jsx
<div className={[condition1 ? 'a-class' : '', !condition1 ? 'another-class' : ''].join(' ')}>...</div>
```

### Style a component with a css file living next to the component

Using webpack, it's pretty easy to inject CSS parts inside a javascript file

```css
.MyComponent-root-style {
  color: red;
  background-color: blue;
}
```

```javascript
import React, { Component } from 'react';
import './MyComponent.css';  // inject css (using webpack)

export class MyComponent extends Component {
  
  render() {
    return (
      <div className="MyComponent-root-style">...</div>
    );
  }
}
```

### Style a component with inline styling

React let you write inline style pretty easily

```javascript
import React, { Component } from 'react';

const Styles = {
  myComponent: {
    color: 'red',
    backgroundColor: 'blue',
    height: 42 // implicit conversion to '42px',
    width: '100%'
  },
  ...
};

export class MyComponent extends Component {
  render() {
    return (
      <div style={Styles.myComponent}>...</div>
    );
  }
}
```

## Conditional display of components

if you want to display component conditionaly, you can use truthy/falsy trick

```javascript
export class MyComponent extends Component {

  render() {
    return (
      <div>
        {this.state.loading && (
          <h2>Loading ...</h2>
        )}
        {!this.state.loading && (
          <h2>Loaded</h2>
        )}
      </div>
    );
  }
}
```

## Add props on `this.props.children`

sometimes you want to write a component that will render its children, but you'd like to add some props to the children.
It's quite useful with `react-router` for instance. To do that your can use `React.cloneElement`

```javascript
import React, { Component } from 'react';

export class MyComponent extends Component {

  render() {
    return (
      <div>
        <h2>{this.props.title}</h2>
        {this.props.children && React.cloneElement(this.props.children, {
          newProps: 'new prop value'
        })}
      </div>
    );
  }
}
```

## Loading data from an HTTP services

If you want to fetch some data when a component is mounted to the dom, use the lifecycle function `componentDidMount`

```javascript
export class MyComponent extends Component {

  state = {
    location: null
  };

  componentDidMount() {
    // it's always a good thing to load data when the component is already monted into the DOM
    // event if it's not http related
    fetch('https://freegeoip.net/json/')
      .then(r => r.json())
      .then(location => this.setState({ location }));
  }

  render() {
    return (
      <div>
        {!this.state.location && (
          <h2>Loading ...</h2>
        )}
        {this.state.location && (
          <pre>{JSON.stringify(this.state.location, null, 2)}</pre>
        )}
      </div>
    );
  }
})
```

## Binding a text input

```javascript
import React, { Component } from 'react';

export class MyComponent extends Component {

  state = {
    content: ''
  };

  onChange = (e) => {
    this.setState({ content: e.target.value });
  };

  sendContent = () => {
    const content = this.state.content;
    this.setState({ content: '' }, () => {
      // do whatever you want with content
    });
  };

  render() {
    return (
      <div>
        <input type="text" value={this.state.content} onChange={this.onChange} />
        <button type="button" onClick={this.sendContent}>Send content</button>
      </div>
    );
  }
}
```
