# To-Do List en React con Redux

Este es un ejemplo básico de cómo crear una aplicación To-Do List en React utilizando Redux para gestionar el estado de las tareas. A continuación, se detallan los pasos necesarios para configurar este proyecto.

## Pasos para configurar el proyecto

### 1. Instalación de dependencias

Asegúrate de tener Node.js y npm instalados. Luego, crea un proyecto de React con Create React App y agrega las dependencias necesarias:

```bash
npx create-react-app todo-list-redux
cd todo-list-redux
npm install redux react-redux

2. Estructura de carpetas
Organiza tu proyecto de la siguiente manera:

src/
├── actions/
│   ├── types.js
│   ├── todoActions.js
├── components/
│   ├── TodoForm.js
│   ├── TodoList.js
├── reducers/
│   ├── todoReducer.js
├── store/
│   ├── index.js
├── App.js
├── index.js

3. Definición de tipos de acciones (types.js):
Crea un archivo types.js para definir tipos de acciones. Esto ayuda a mantener un registro de las acciones disponibles.

// actions/types.js
export const ADD_TODO = 'ADD_TODO';
export const REMOVE_TODO = 'REMOVE_TODO';

4. Acciones (todoActions.js):
Define las acciones en todoActions.js para agregar y eliminar tareas.

// actions/todoActions.js
import { ADD_TODO, REMOVE_TODO } from './types';

// Acción para agregar una tarea
export const addTodo = (text) => ({
  type: ADD_TODO,
  payload: {
    text,
  },
});

// Acción para eliminar una tarea
export const removeTodo = (id) => ({
  type: REMOVE_TODO,
  payload: {
    id,
  },
});

5. Reducer (todoReducer.js):
Crea el reducer en todoReducer.js para gestionar el estado de las tareas y responder a las acciones.

// reducers/todoReducer.js
import { ADD_TODO, REMOVE_TODO } from '../actions/types';

const initialState = {
  todos: [],
};

const todoReducer = (state = initialState, action) => {
  switch (action.type) {
    case ADD_TODO:
      return {
        ...state,
        todos: [...state.todos, { id: Date.now(), text: action.payload.text }],
      };
    case REMOVE_TODO:
      return {
        ...state,
        todos: state.todos.filter((todo) => todo.id !== action.payload.id),
      };
    default:
      return state;
  }
};

export default todoReducer;

6. Configuración del almacenamiento (store/index.js):
Combina el reducer y crea el almacenamiento Redux.

// store/index.js
import { createStore } from 'redux';
import todoReducer from '../reducers/todoReducer';

const store = createStore(todoReducer);

export default store;

7. Componente Formulario (TodoForm.js):
Crea el componente TodoForm.js para agregar nuevas tareas.

// components/TodoForm.js
import React, { useState } from 'react';
import { useDispatch } from 'react-redux';
import { addTodo } from '../actions/todoActions';

const TodoForm = () => {
  // ...
};

export default TodoForm;

8. Componente Lista de Tareas (TodoList.js):
Crea el componente TodoList.js para mostrar las tareas y permitir la eliminación.

// components/TodoList.js
import React from 'react';
import { useSelector, useDispatch } from 'react-redux';
import { removeTodo } from '../actions/todoActions';

const TodoList = () => {
  // ...
};

export default TodoList;

9. Integración en la aplicación principal (App.js):
Conecta los componentes al almacenamiento Redux en App.js.

// App.js
import React from 'react';
import './App.css';
import TodoForm from './components/TodoForm';
import TodoList from './components/TodoList';

function App() {
  // ...
}

export default App;

10. Conexión de la aplicación principal a Redux (index.js):
Proporciona el almacenamiento Redux a toda la aplicación en index.js.

// index.js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import { Provider } from 'react-redux';
import store from './store';

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
);

