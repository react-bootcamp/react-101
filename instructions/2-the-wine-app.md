# The "Open Wine Database" app

In this step, we will create a React application to browse wine regions and give some details about wines.

Take a look at the wireframe of the app :

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

Before you start coding, there are few questions to ask :

* Which are the components of the app and what is the hierarchy between components?
* What is the data managed by each component? Should I manage the data with `props` or with `state`?
* Ho do my components communicate? Which events should I manage?
* Once I'm ready, how to start coding the app?

## Component hierarchy

The first thing to do is to *"Think React"* :-)

From the wireframe we can identify sevral components :

* `Regions`: the component that manages the list of wine regions (left column)
* `WineList`: the component that manages the list of the wines of the selected region (middle column)
* `Wine`: the component that manages the details of the selected wine (right column)
* `WineApp`: this is a sort of parent component, that assemble the other components. This is our application!

<img src='https://github.com/react-bootcamp/react-101/raw/master/instructions/img/wine-app-mockup-components.png' width='800' alt='The Wine App Wireframe'>

## Props and state

## Communication between components

## How to start coding?
