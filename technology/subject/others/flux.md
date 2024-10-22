Here are some **React Flux code snippets** along with a **quiz** to test your knowledge of the Flux architecture pattern.

### React Flux Code Snippets

#### 1. **Action Creator**
Action creators are functions that create actions, which are simple JavaScript objects containing information to describe the change.

```js
// actions/TodoActions.js
import dispatcher from '../dispatcher';

export function addTodoItem(text) {
  dispatcher.dispatch({
    type: 'ADD_TODO',
    text,
  });
}

export function removeTodoItem(id) {
  dispatcher.dispatch({
    type: 'REMOVE_TODO',
    id,
  });
}
```

#### 2. **Dispatcher**
The dispatcher is a central hub that manages actions and sends them to the stores. It’s a singleton and controls the data flow.

```js
// dispatcher.js
import { Dispatcher } from 'flux';

const dispatcher = new Dispatcher();

export default dispatcher;
```

#### 3. **Store**
Stores hold the application state and logic. Stores respond to actions sent by the dispatcher and update their data accordingly.

```js
// stores/TodoStore.js
import { EventEmitter } from 'events';
import dispatcher from '../dispatcher';

class TodoStore extends EventEmitter {
  constructor() {
    super();
    this.todos = [];
  }

  getAll() {
    return this.todos;
  }

  handleActions(action) {
    switch (action.type) {
      case 'ADD_TODO':
        this.todos.push({ id: Date.now(), text: action.text });
        this.emit('change');
        break;

      case 'REMOVE_TODO':
        this.todos = this.todos.filter(todo => todo.id !== action.id);
        this.emit('change');
        break;

      default:
        break;
    }
  }
}

const todoStore = new TodoStore();
dispatcher.register(todoStore.handleActions.bind(todoStore));

export default todoStore;
```

#### 4. **React Component**
The React component subscribes to store updates and renders the data.

```js
// components/TodoList.js
import React, { Component } from 'react';
import TodoStore from '../stores/TodoStore';
import * as TodoActions from '../actions/TodoActions';

class TodoList extends Component {
  constructor() {
    super();
    this.state = {
      todos: TodoStore.getAll(),
    };
  }

  componentDidMount() {
    TodoStore.on('change', this.updateTodos.bind(this));
  }

  componentWillUnmount() {
    TodoStore.removeListener('change', this.updateTodos.bind(this));
  }

  updateTodos() {
    this.setState({
      todos: TodoStore.getAll(),
    });
  }

  addTodo() {
    const todoText = prompt('Enter a new todo:');
    TodoActions.addTodoItem(todoText);
  }

  removeTodo(id) {
    TodoActions.removeTodoItem(id);
  }

  render() {
    const todoItems = this.state.todos.map(todo => (
      <li key={todo.id}>
        {todo.text}
        <button onClick={() => this.removeTodo(todo.id)}>Delete</button>
      </li>
    ));

    return (
      <div>
        <button onClick={this.addTodo}>Add Todo</button>
        <ul>{todoItems}</ul>
      </div>
    );
  }
}

export default TodoList;
```

### Quiz on React Flux Architecture

1. **What is the main role of the dispatcher in Flux architecture?**
   - A) To render React components
   - B) To register and manage actions
   - C) To handle state management
   - D) To propagate actions to the stores

2. **Which of the following correctly describes the purpose of a store in Flux?**
   - A) It creates actions and sends them to the dispatcher.
   - B) It holds and manages the state of the application.
   - C) It dispatches actions to components.
   - D) It handles routing within the application.

3. **What event does a store usually emit when it changes state?**
   - A) `dispatch`
   - B) `register`
   - C) `change`
   - D) `update`

4. **In the context of Flux, what is an action?**
   - A) A method that is executed inside a component
   - B) A plain JavaScript object with a `type` and additional data
   - C) An event listener for user input
   - D) A function that directly modifies the DOM

5. **How does a React component subscribe to updates from a store?**
   - A) By registering a listener with the store’s `emit()` method.
   - B) By using React’s `onUpdate()` lifecycle method.
   - C) By calling the store’s `on()` method and passing a callback function.
   - D) By dispatching an action directly to the store.

6. **What would happen if a store does not handle an action in Flux architecture?**
   - A) The action is automatically handled by the dispatcher.
   - B) The action is ignored, and no state change occurs.
   - C) The action is passed to the next store.
   - D) An error is thrown.

### Quiz Answers:
1. D) To propagate actions to the stores
2. B) It holds and manages the state of the application.
3. C) `change`
4. B) A plain JavaScript object with a `type` and additional data
5. C) By calling the store’s `on()` method and passing a callback function.
6. B) The action is ignored, and no state change occurs.

These code snippets and quiz questions should provide a clearer understanding of the basic principles of Flux architecture in a React application.