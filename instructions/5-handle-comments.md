# Add 'comments' support

In this step, we are only going to read comments from the Wine API.

## The Wine API

For this step you'll need to fetch `comments` data from the API exposed at `https://wines-api.herokuapp.com`.

The URL you need are the following

* `GET  https://wines-api.herokuapp.com/api/wines/:id/comments` => returns a comment object

Obviously, you'll need to add the following functions to the module responsible for calling the API

```javascript
export function fetchComments(id) {
  ...
}
```

## The `<CommentList />` component

The  `<CommentList />` will be added in the `card-action` section and will have the following contract

```javascript
import React, { Component } from 'react';
import PropTypes from 'prop-types';

export class CommentList extends Component {

  static propTypes = {
    wine: PropTypes.object
  };

  state = {
    comments: []
  };
  ...
}
```

the view of `<CommentList />` will look something like

```html
<div>
  <!-- here the title is only displayed if there is at least one comment -->
  <h5>Comments</h5>
  <Comment ... />
  <Comment ... />
  <Comment ... />
</div>
```

We can see that the comment list will use another component to display each comment

## The `<Comment />` component

The `<Comment />` component will have the following contract

```javascript
import React, { Component } from 'react';
import PropTypes from 'prop-types';

export class Comment extends Component {
  static propTypes = {
    comment: PropTypes.object
  };
  ...
});
```

the view of `<Comment />` component will look something like

```html
<p class="comment" data-title="title of the comment" data-date="date of the comment">
  A very nice comment
</p>
```

## What it should look like

And now your wine details component should look something like that (without the blue and red outline of course)

<img src='https://github.com/react-bootcamp/react-101/raw/master/instructions/img/comments.png' width='800' alt='The comments section'>

# What's next

Now you're ready to add third party JS lib to the Wine application. Go to the [next step](./6-integrate-with-third-party-apis.md) to start writing it.
