# Integrate a third-party library

Here we are going to use the modal component from `materialize` to add comments on a wine

## The Wine API

For this step you'll need to add `comments` to the API exposed at `https://wines-api.herokuapp.com`.

The URL you need are the following

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
```

## The `<CommentButton />` component

## The `<CommentModal />` component

## What it should look like

And now your wine details component should look something like that

<img src='https://github.com/react-bootcamp/react-101/raw/master/instructions/img/addcomment.gif' width='800' alt='Add comment'>

# What's next

`react-101` is now over. See you soon for `react-102` ;-)
