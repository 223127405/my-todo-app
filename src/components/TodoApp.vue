<template>
  <div id="app">
    <h1>Todo App</h1>

    <!-- Input for adding new todo items -->
    <div class="input-container">
      <input v-model="newTodo" @keyup.enter="addTodo" type="text" placeholder="Add a new task">
    </div>

    <!-- List of todo items -->
    <ul class="todo-list">
      <li v-for="(todo, index) in todos" :key="index" class="todo-item">
        <input type="checkbox" v-model="todo.completed">
        <span :class="{ completed: todo.completed }">{{ todo.text }}</span>
        <button @click="removeTodo(index)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodo: '',
      todos: []
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() !== '') {
        this.todos.push({ text: this.newTodo, completed: false });
        this.newTodo = '';
      }
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    }
  }
};
</script>

<style>
:root {
  --primary-color: #3498db;
  --secondary-color: #2ecc71;
}

#app {
  font-family: 'Roboto', sans-serif;
  font-size: 16px;
  text-align: center;
  margin-top: 60px;
  background-image: linear-gradient(to bottom, var(--primary-color), var(--secondary-color));
  color: white;
  padding: 20px;
}

.input-container {
  margin-bottom: 20px;
}

.todo-list {
  list-style: none;
  padding: 0;
}

.todo-item {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
  background-color: rgba(255, 255, 255, 0.1);
  border-radius: 5px;
  padding: 10px;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.2);
  transition: background-color 0.2s ease-in-out;
}

.todo-item:hover {
  background-color: rgba(255, 255, 255, 0.2);
}

.todo-list input[type="checkbox"] {
  margin-right: 10px;
  transition: transform 0.2s ease-in-out;
}

.todo-list input[type="checkbox"]:hover {
  transform: scale(1.1);
}

.completed {
  text-decoration: line-through;
}

button {
  background-color: var(--primary-color);
  color: white;
  border: none;
  padding: 5px 10px;
  cursor: pointer;
  transition: background-color 0.2s ease-in-out;
}

button:hover {
  background-color: var(--secondary-color);
}
</style>
