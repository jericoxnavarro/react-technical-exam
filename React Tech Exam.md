# Question #1 - React - Identify the Problem and Refactor

Please identify the problems and tell us what the problems are, then improve this React Component by coding your own version!

It would be a plus point if you can convert/refactor them into React hooks.

### Old code:

```jsx
class MyComponent extends React.Component {
  constructor(props) {
    // set the default internal state
    this.state = {
      clicks: 0,
    };
  }

  componentDidMount() {
    this.refs.myComponentDiv.addEventListener('click', this.clickHandler);
  }

  componentWillUnmount() {
    this.refs.myComponentDiv.removeEventListener('click', this.clickHandler);
  }

  clickHandler() {
    this.setState({
      clicks: this.clicks + 1,
    });
  }

  render() {
    let children = this.props.children;

    return (
      <div className="my-component" ref="myComponentDiv">
        <h2>My Component ({this.state.clicks} clicks})</h2>
        <h3>{this.props.headerText}</h3>
        {children}
      </div>
    );
  }
}
```

### My Answer

##### Identified Problems

1. The component is implemented as a class based component which is not already recommended in creating react applications. We can use functional components, which is a more modern and concise way to manage state and side effects.
2. The **`ref`** attribute is React is generally not recommended to use. We can use onClick for click triggers.
3. The **`clickHandler`** function is not bound to the component instance, resulting in an error when trying to call **`this.setState`** inside the function.

##### Refactored Code

```jsx
import React, { useState } from 'react';

function MyComponent({ headerText, children }) {
  const [clicks, setClicks] = useState(0);

  const handleClick = () => {
    setClicks((prevClicks) => prevClicks + 1);
  };

  return (
    <div className="my-component" onClick={handleClick}>
      <h2>My Component ({clicks} clicks)</h2>
      <h3>{headerText}</h3>
      {children}
    </div>
  );
}

export default MyComponent;
```

# Question #2 - React - Solve the Problem

Complete the following <TodoList> component to display todos and allow for adding and removing of todo items

### Old code:

```jsx
const todosReducer = (state, action) => {
  switch (action.type) {
    case 'ADD_TODO':
    case 'REMOVE_TODO':
  }
};

const TodoList = () => {
  const [todos, dispatch] = useReducer(todosReducer, []);

  return (
    <div>
      <ul>
        {todos.map((todo) => (
          <li>
            <button>Remove todo</button>
          </li>
        ))}
      </ul>
      <button>Add todo</button>
    </div>
  );
};
```

### My Answer

1. Update the todosReducer function to handle ADD_TODO and REMOVE_TODO actions.
2. Implement event handlers for adding and removing todos.

##### Refactored Code

```jsx
import React, { useReducer, useState } from 'react';

const todosReducer = (state, action) => {
  switch (action.type) {
    case 'ADD_TODO':
      return [...state, action.payload];
    case 'REMOVE_TODO':
      return state.filter((todo) => todo.id !== action.payload);
    default:
      return state;
  }
};

const TodoList = () => {
  const [todos, dispatch] = useReducer(todosReducer, []);
  const [todoText, setTodoText] = useState('');

  const handleAddTodo = () => {
    if (todoText !== '') {
      const newTodo = {
        id: Date.now(), // Can use any unique ID
        text: todoText,
      };
      dispatch({ type: 'ADD_TODO', payload: newTodo });
      setTodoText('');
    }
  };

  const handleRemoveTodo = (todoId) => {
    dispatch({ type: 'REMOVE_TODO', payload: todoId });
  };

  return (
    <div>
      <ul>
        {todos.map((todo) => (
          <li key={todo.id}>
            {todo.text}
            <button onClick={() => handleRemoveTodo(todo.id)}>Remove todo</button>
          </li>
        ))}
      </ul>
      <div>
        <input type="text" value={todoText} onChange={(e) => setTodoText(e.target.value)} placeholder="Enter a new todo" />
        <button onClick={handleAddTodo}>Add todo</button>
      </div>
    </div>
  );
};

export default TodoList;
```
