# Add 'comments' support

## The Wine API

For this step you'll need to fetch `comments` data from the API exposed at `https://wines-api.herokuapp.com`.

The URL you need are the following

* `GET  https://wines-api.herokuapp.com/api/wines/:id/comments` => returns a comment object
* `POST https://wines-api.herokuapp.com/api/wines/:id/comments` => add a comment on the wine

Obviously, you'll need to add the following functions to the module responsible for calling the API

```javascript
export function commentWine(id, content) {
  return fetch(`${host}/api/wines/${id}/comments`, {
    method: 'POST',
    headers: {
      'Accept': 'application/json',
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({ title: 'The title', content })
  });
}

export function fetchComments(id) {
  ...
}
```

## The `<CommentList />` component

The  `<CommentList />` will be added in the `card-action` section.

## The `<Comment />` component

## What it should look like

And now your wine details component should look something like that

<img src='https://github.com/react-bootcamp/react-101/raw/master/instructions/img/comments.png' width='800' alt='The comments section'>

# What's next

Now you're ready to add third party JS lib to the Wine application. Go to the [next step](./6-6-integrate-with-third-party-apis.md) to start writing it.
