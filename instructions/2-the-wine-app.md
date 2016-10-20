# The "Open Wine Database" app

In this step, we will create a React application to browse wine regions and give some details about wines.

Take a look at the wireframe of the app:

* The first column contains the wine regions. A click on a region changes the content of the second column.
* The second column is the list of the wines of the selected region. A click on a wine changes the content of the third column.
* The third column contains all the details of the selected wine :
  * name
  * robe (red, white, rosé...)
  * appellation
  * grapes
  * picture

<img src='https://github.com/react-bootcamp/react-101/raw/master/instructions/img/wine-app-mockup.png' width='800' alt='The Wine App Wireframe'>

## Let's go!

Before you start coding, there are few questions to ask:

* Which are the components of the app and what is the hierarchy between components?
* What is the data managed by each component? Should I manage the data with `props` or with `state`?
* How do my components interact? Which events should I manage?
* Once I'm ready, how to start coding the app?

## Component hierarchy

The first thing to do is to ***"Think React"*** :-)

From the wireframe we can identify sevral components:

* `Regions`: the component that manages the list of wine regions (left column)
* `WineList`: the component that manages the list of the wines of the selected region (middle column)
* `Wine`: the component that manages the details of the selected wine (right column)
* `WineApp`: this is a sort of parent component, a container that assemble the other components.

<img src='https://github.com/react-bootcamp/react-101/raw/master/instructions/img/wine-app-mockup-components.png' width='800' alt='The Wine App Wireframe'>

## Props and state

The data managed by the wine application are:

* the list of wine regions
* the selected region
* the list of the wines of the selected region
* the selected wine (and its details)

So, should we use `props` or `state` to store these data in our components?
The solution is quite easy!
Because the component `props` are immutable and the component `state` is mutable, we usually define two types of components in a React app:

* **Dumb components**: they are also called *Presentational components* and are concerned with *how things look*. They use `props` only.
* **Smart components**: they are also called *Container components* and are concerned with *how things work*. They use `state`.

Feel free to read this [great post about Smart and Dumb components](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0#.a0czhe4g8).

In our React application, `Regions`, `WineList` and `Wine` are Dumb Components (presentational stuff only),they only use their `props`. `WineApp` is a Dumb Component, aka the container that will make the Dumb Components work together. It uses its `state`.

## Interaction between components

Interaction between components are:

* A click on a wine region loads the wines of the region (in the middle column) and the details of the first wine of the region (in the right column).
* A click on a wine loads the detail of the wine (int the right column).

## How to start coding?

A good way to start building a React application is:

* Build a static version of the app by creating each component identified in the step "Thinking React"
* Define an initial state for each *Smart Component* and use this state in component rendering.
* Manage events so that the app become interactive.

### Static version of the app

#### Dumb components

Create all *Dumb Components*: `Regions`, `WineList` and `Wine` and implement the `render()` method for each one, based on the component `props`.

##### `Regions`

The `<Regions />` component just display a list of regions. The contract of the `<Regions />` component is the following

```javascript
import React, { PropTypes } from 'react';

export const Regions = React.createClass({
  propTypes: {
    onSelectRegion: PropTypes.func,
    regions: PropTypes.array, // an array of string
    region: PropTypes.object // the selected region
  },
  ...
});
```

the view of `<Regions />` component will look something like

```html
<div class="col s12 m6 l3">
  <h2 class="center-align">Regions</h2>
  <div class="collection">
    <a href="#!"class="collection-item">Bordeaux</a>
    <a href="#!"class="collection-item active">Champagne</a>
  </div>
</div>
```

##### `WineList`

The `<WineList />` component display a list of wine for the selected region. The contract of the `<WineList />` component is the following

```javascript
import React from 'react';

export const WineList = React.createClass({
  propTypes: {
    onSelectWine: PropTypes.func,
    wines: PropTypes.array, // an array of wine object
    wine: PropTypes.object // the selected wine
  },
  ...
});
```

the view of `<WineList />` component will look something like

```html
<div class="col s12 m6 l3">
  <h2 class="center-align">Wines</h2>
  <div class="collection">
    <a href="#!" class="collection-item">Wine 1</a>
    <a href="#!" class="collection-item active">Wine 2</a>
    <a href="#!" class="collection-item">Wine 3</a>
  </div>
</div>
```

##### `Wine`

The `<Wine />` component display a list of wine for the selected region. The contract of the `<Wine />` component is the following

```javascript
import React from 'react';

export const Wine = React.createClass({
  propTypes: {
    wine: PropTypes.object, // the wine object
  },
  ...
});
```

the view of `<Wine />` component will look something like

```html
<div class="col s12 m12 l6">
  <h2 class="center-align">Wine details</h2>
  <div class="card horizontal">
    <div class="card-image">
      <img class="responsive-img wine-detail-image" alt="Wine bottle pic" src="https://wines-api.herokuapp.com/api/wines/wine1/image" />
    </div>
    <div class="card-stacked">
      <div class="card-content">
        <h3>Name of the Wine</h3>
        <br/>
        <p><b>Appellation:</b> Wine appelation name</p>
        <p><b>Region:</b> Wine appelation region</p>
        <p><b>Color:</b> Wine type</p>
        <p><b>Grapes:</b> Wine grape 1, Wine grape 2</p>
      </div>
      <div class="card-action"></div>
    </div>
  </div>
</div>
```

#### Smart components

`<WineApp />` is the only *Smart Component* in our wine app, it assembles the the whole *Dumb Components* created above.

The `<WineApp />` component should look like this:

```html
<div className="container">
  <h1 className="center-align">Open Wine Database</h1>
  <div className="row">
    <Regions ... />
    <WineList ... />
    <Wine ... />
  </div>
</div>
```
