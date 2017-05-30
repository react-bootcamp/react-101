# Connect the app with the Wine API

## The Wine API

For this step you'll need to fetch some data to feed your app. You will you the API exposed at `https://wines-api.herokuapp.com`.

The URL you need are the following

* `GET https://wines-api.herokuapp.com/api/regions` => returns an array of regions (string)
* `GET https://wines-api.herokuapp.com/api/wines?region=:region` => returns an array of wines
* `GET https://wines-api.herokuapp.com/api/wines/:id` => returns a wine

The HTTP client you will use is `fetch`. It's the new standard way to fetch data over http in the browser. Here we use the `whatwg-fetch` npm module to polyfill `fetch` if necessary.

You can find some doc about `fetch` here

* https://www.npmjs.com/package/whatwg-fetch
* https://fetch.spec.whatwg.org/
* https://github.github.io/fetch/
* https://github.com/github/fetch

**WARNING**: `fetch` makes heavy usage of Javascript `Promise`. You can read more about it [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)

## Unidirectional data flow

As explained in the previous step, here we will make heavy usage of the unidirectional data flow pattern. The global state of the app will be stored in the highest component of the component tree. The data will be passed to the children as props. Each time the global state will mutate, the `<WineApp />` component will be redraw and all the children components will be updated.

One of the issue with that pattern is that children components will need to trigger state mutation in the root component. To do that, just pass state mutation function to the children component as props in depth.

```javascript
import React, { Component } from 'react';

class App extends Component {
  state = {    // the state of the app
    count: 0
  };

  incrementCounter = () => { // the state mutator function
    this.setState({ count: this.state.count + 1 });
  };

  render() {
    return (
      <div>
        <h1>the count is : {this.state.count}</h1>
        <IncrementButton
          count={this.state.count} // pass state as props
          incrementCounter={this.incrementCounter} /> // pass state mutator as props
      </div>
    );
  }
}

class IncrementButton extends Component {
  render() {
    return (
      <button type="button" onClick={this.props.incrementCounter}>{this.props.count} + 1</button>
    );
  }
}
```

## How to start

First, write a new module to expose all the methods to fetch data from the Open Wine Database API. The module will look something like that

```javascript
export function fetchRegions() {
  return fetch(`https://wines-api.herokuapp.com/api/regions`).then(r => r.json());
}

export function fetchWinesFrom(region) {
  ...
}

export function fetchWine(id) {
  ...
}
```

then, add new functions on the `<WineApp />` component to call that module and mutate the `<WineApp />` state.

```javascript
import * as WinesService from '../services/wines';

export class WineApp extends Component {
  state = {
    regions: [],
    selectedRegion: null,
    wines: [],
    selectedWine: null,
  };

  componentDidMount() {
    // load regions and maybe wines from the first region
  }

  onSelectRegion = (region) => {
    // load wines from the selected region
  };

  onSelectWine = (id) => {
    // load wine details from wine id
  };

  render() {
    ...
  }
}
```

now, just pass the data from the state and useful functions to the child components, add the right event listeners on elements, and it should be good.

Your app should work just like that

<img src='https://github.com/react-bootcamp/react-101/raw/master/instructions/img/appworking.gif' width='800' alt='First run'>

# What's next

Now you're ready to add support of likes to the Wine application. Go to the [next step](./4-handle-likes.md) to start writing it.
