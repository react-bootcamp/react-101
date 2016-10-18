# React 101

React 101 is a workshop for those that want to learn React.js and its ecosystem, step by step.

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons Licence" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a>

<span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">react-101</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="https://github.com/react-bootcamp/react-101" property="cc:attributionName" rel="cc:attributionURL">Mathieu ANCELIN and Sébastien PRUNIER</a> is distributed under the terms of the <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons - Attribution - NonCommercial - ShareAlike</a>.

## The "Open Wine Database" app

during the workshop you will create a webapp to manage your favorite wines* !
The main feature of the app are

* List the wine by regions
* Display the details of a specific wine
* Like a wine
* Add comments on a wine

\* *Alcohol abuse is dangerous for health, consume with moderation;-)*

## Technical requirements

the technical requirements are the following

* Node (version 5.x or 6.x) with NPM (at least version 3.x)
* Git
* A text editor (if you don't have one, just use Atom)
* React Developer Tools

### Node

Node is the first requirement for the workshop. You need to install at least version 5.x and version 3.x for `npm`. You can get it on the official website at [https://nodejs.org/en/download/](https://nodejs.org/en/download/)

You can verify your current version of `node` and `npm` by running the following commands :

```sh
$ node -v
v6.6.0

$ npm -v
3.10.7
```

you can upgrade an existing version of npm by running the following command :

```sh
npm update -g npm
```

### Git

Download and install the appropriate version of Git on your OS, follow the instructions available on the official website: [https://git-scm.com/downloads](https://git-scm.com/downloads)

Verify the installation by running the following command in a terminal:

```sh
$ git --version
git version 2.8.4
```

### Atom

If you don't have a favorite text editor to write Javascript application, we advise you to use [Atom](https://atom.io).

Download and install Atom and install the following packages:

* language-javascript-jsx
* linter-eslint

To learn how to manage Atom packages:
 https://atom.io/docs/latest/using-atom-atom-packages

### React Developer Tools

In order to have specific tools to react in your web browser, install **React Developer Tools** :

* [React Developer Tools for Google Chrome](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)
* [React Developer Tools for Mozilla Firefox](https://addons.mozilla.org/fr/firefox/addon/react-devtools/)

## Install dependencies

To install the project dependencies, just run the following command in the project:

```sh
npm install
# or if you have `yarn` installed
# yarn install
```

### Open Wine API

The Wine Management application uses a REST API as a data source for it to display wines by regions, with their details, a photo of the bottle, etc ... This API is actually a small server NodeJS / Express with memory data available in the aPI folder. For all stages of the workshop you will need this API to power your application. So you can already start the API server in a separate tab for your device so that it is always available.

To start the server exposing the API, run the following commands:

$ Cd api
$ Npm install
$ Npm start
Then go to http: // localhost: 3000 to explore the documentation of the different routes available. We recommend that you go at least once on this documentation to get an overall idea of ​​the data provided by the API to power your application.


### Common React Patterns

### Steps

* [Step 0 : create the app](./instructions/0-create-the-app.md)
* [Step 1 : write your first React component](1-your-first-component.md)
* [Step 2 : write a first static version of the Open Wine Database app](2-the-wine-app.md)
* [Step 3 : use the Open Wine API to feed the app](3-connect-with-the-wine-api.md)
* [Step 4 : add support for likes](4-handle-likes.md)
* [Step 5 : add support for comments](5-handle-comments.md)
* [Step 6 : integrates a third party JS library](6-integrate-with-third-party-apis.md)
