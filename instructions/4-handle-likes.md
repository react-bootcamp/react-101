# Add 'likes' support

## The Wine API

For this step you'll need to fetch `likes` data from the API exposed at `https://wines-api.herokuapp.com`.

The URL you need are the following

* `GET  https://wines-api.herokuapp.com/api/wines/:id/like` => returns an object with a boolean property named `like`
* `POST https://wines-api.herokuapp.com/api/wines/:id/like` => change the `like` status of the wine

Obviously, you'll need to add the following functions to the module responsible for calling the API

```javascript
export function likeWine(id) {
  return fetch(`${host}/api/wines/${id}/like`, {
    method: 'POST',
    headers: {
      'Accept': 'application/json',
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({ like: true })
  });
}

export function unlikeWine(id) {
  ...
}

export function isWineLiked(id) {
  ...
}
```

## The `<LikeButton />` component

Now, you have to write a new component to display the `like` button into a `<Wine />` component. The button will be added in the `card-action` section. This component will have the following contract

```javascript
import React, { Component } from 'react';
import PropTypes from 'prop-types';

export class LikeButton extends Component {

  static propTypes = {
    wine: PropTypes.object
  };

  state = {
    liked: false
  };
  ...
});
```

when the wine is unliked, the button must look something like the following snippet

```html
<a class="waves-effect waves-teal btn-flat">
  <span>Like <i class="material-icons left">thumb_up</i></span>
</a>
```

when the wine is liked, the button must look something like the following snippet

```html
<a class="waves-effect waves-teal btn-flat">
  <span>Unlike <i class="material-icons left">thumb_down</i></span>
</a>
```

If you need to react to the change of a property value in a component, you can use the `componentWillReceiveProps` function

```javascript
import React, { Component } from 'react';
import PropTypes from 'prop-types';

export class LikeButton extends Component {

  static propTypes = {
    wine: PropTypes.object
  };

  state = {
    liked: false
  };

  componentWillReceiveProps(nextProps) {
    if (nextProps.wine !== this.props.wine) {
      ...
    }
  }
  ...
}
```
## What it should look like

And now your like button component should look something like that

<img src='https://github.com/react-bootcamp/react-101/raw/master/instructions/img/like.gif' width='800' alt='The like button'>

# What's next

Now you're ready to add support for comments to the Wine application. Go to the [next step](./5-handle-comments.md) to start writing it.
