# Connect the app with the Wine API

## The Wine API

For this step you'll need to fetch some data to feed your app. You will you the API exposed at `https://wines-api.herokuapp.com`.

The URL you need are the following

* `https://wines-api.herokuapp.com/api/regions` => returns an array of regions (string)
* `https://wines-api.herokuapp.com/api/wines?region=:region` => returns an array of wines
* `https://wines-api.herokuapp.com/api/wines/:id` => returns a wine

## Unidirectional data flow

State at the root of the tree, pass data and mutators as props to children in depth

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

export const WineApp = React.createClass({
  getInitialState() {
    return {
      regions: [],
      selectedRegion: null,
      wines: [],
      selectedWine: null,
    };
  },
  componentDidMount() {
    // load regions and maybe wines from the first region
  },
  onSelectRegion(region) {
    // load wines from the selected region
  },
  onSelectWine(id) {
    // load wine details from wine id
  },
  render() {
    ...
  }
});
```

now, just pass the data from the state and useful functions to the child components, add the right event listeners on elements, and it should be good.

Your app should work just like that

<img src='https://github.com/react-bootcamp/react-101/raw/master/instructions/img/appworking.png' width='800' alt='First run'>

# What's next

Now you're ready to add support of likes to the Wine application. Go to the [next step](./4-handle-likes.md) to start writing it.
