<template>
  <div id='app'>
    <h1>Todo App</h1>
    <todo-list v-bind:todos="todos"/>
    <create-todo v-on:create-todo="addTodo"/>
  </div>
</template>

<script>
import TodoList from './components/TodoList';
import CreateTodo from './components/CreateTodo';

export default {
  name: 'App',
  components: {
    TodoList,
    CreateTodo,
  },

  data() {
    return {
      todos: [
        { title: 'Todo A', project: 'Project A', done: false },
        { title: 'Todo B', project: 'Project B', done: true },
        { title: 'Todo C', project: 'Project C', done: false },
      ],
    };
  },

  methods: {
    addTodo(newTodo) {
      this.todos.push(newTodo);
      swal('Success!', 'Todo created', 'success');
    },
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
