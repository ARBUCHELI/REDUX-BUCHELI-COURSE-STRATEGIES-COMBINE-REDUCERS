# REDUX-BUCHELI-COURSE-STRATEGIES-COMBINE-REDUCERS

## REDUX-LESSONS-INSTRUCTOR-ANDRES-R.-BUCHELI

## Usage:

In the reducer composition pattern, the same steps are taken by the rootReducer for each slice reducer:

* call the slice reducer with its slice of the state and the action as arguments

* store the returned slice of state in a new object that is ultimately returned by the rootReducer().

```
import { createStore } from 'redux';
 
// todosReducer and filterReducer omitted
 
const rootReducer = (state = {}, action) => {
  const nextState = {
    todos: todosReducer(state.todos, action),
    filter: filterReducer(state.filter, action)
  };
  return nextState;
};
 
const store = createStore(rootReducer);
```

The Redux package helps facilitate this pattern by providing a utility function called combineReducers() which handles this boilerplate for us:

```
import { createStore, combineReducers } from 'redux'
 
// todosReducer and filterReducer omitted.
 
const reducers = {
    todos: todosReducer,
    filter: filterReducer
};
const rootReducer = combineReducers(reducers);
const store = createStore(rootReducer);
```

Let’s break this code down:

* The reducers object contains the slice reducers for the application. The keys of the object correspond to the name of the slice being managed by the reducer value.
* The combineReducers() function accepts this reducers object and returns a rootReducer function.
* The returned rootReducer is passed to createStore() to create a store object.

Just as before, when an action is dispatched to the store, the rootReducer() is executed which then calls each slice reducer, passing along the action and the appropriate slice
of state.

The last 6 lines of this example can be rewritten inline:

```
const store = createStore(combineReducers({
    todos: todosReducer,
    filter: filterReducer
}));
```
Take a look at store.js where you will find the slice reducers that you created in the last exercise. Now, however, the rootReducer() is missing. Rather than creating this 
function by hand, you will use combineReducers().
