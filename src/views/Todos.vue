<template>
  <div>
    <h2>Todo application</h2>
    <router-link to="/">Home</router-link>
    <hr />
    <AddTodo @add-todo="addTodo" />
    <hr />
    <TodoList v-bind:todos="todos" @remove-todo="removeTodo" />
  </div>
</template>

<script>
import TodoList from "@/components/TodoList";
import AddTodo from "@/components/AddTodo";

export default {
  name: "App",
  data() {
    return {
      todos: [
        { id: 1, title: "Купить хлеб", complated: false },
        { id: 2, title: "Купить молоко", complated: false },
        { id: 3, title: "Купить воду", complated: false }
      ]
    };
  },
  mounted() {
    fetch("https://jsonplaceholder.typicode.com/todos?_limit=5")
      .then(response => response.json())
      .then(json => {
        this.todos = json;
      });
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(t => t.id !== id);
    },
    addTodo(todo) {
      this.todos.push(todo);
    }
  },
  components: {
    TodoList,
    AddTodo
  }
};
</script>