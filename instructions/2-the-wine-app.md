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

The `Region` component should look like this:

```html
<div className="col s12 m6 l3">
  <h2 className="center-align">Regions</h2>
  <div className="collection">
    {this.props.regions.map(region =>
      <a key={region}
        href="#!"
        onClick={e => this.onSelectRegion(e, region)}
        className={['collection-item', region === this.props.region ? 'active' : ''].join(' ')}>
          {region}
      </a>
    )}
  </div>
</div>
```

##### `WineList`

##### `Wine`

#### Smart components

`WineApp` is the only *Smart Component* in our wine app, it assembles the the whole *Dumb Components* created above.

The `WineApp` component should look like this:

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
