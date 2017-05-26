# Redux dynamics
A collection of useful methods and tools to make your [Redux](http://redux.js.org/) workflow slightly more dynamic.

## Methods
### `createReducer(initialState<Object>, actions<Array>)`
* Simplifies declaration of `initialState`
* Enforces immutability of the state
* State is always an instance of [Immutable Record](https://facebook.github.io/immutable-js/docs/#/Record), which provides [certain benefits](https://tonyhb.gitbooks.io/redux-without-profanity/using_immutablejs_records.html)
* Scoped variables and logic (compared to `switch` statements where you cannot have multiple variables with the same name under single reducer)
* No need to explicitly return state, it is always returned by default (in case not modified by any action)
```js
import { createReducer } from 'redux-dynamics';

export default createReducer({
  initialState: {
    isFetching: false,
    author: undefined,
    postCount: 0
  },
  actions: [
    {
      type: 'GET_AUTHOR_REQUEST',
      reducer: state => state.set('isFetching', true)
    },
    {
      type: 'GET_AUTHOR_SUCCESS',
      reducer: (state, action) => state.set('author', action.payload.body)
      }
    },
    {
      type: ['GET_AUTHOR_SUCCESS', 'GET_AUTHOR_ERROR'],
      reducer: state => state.set('isFetching', false)
    }
  ]
});
```
