<template>
  <div class="hello">
    <Header />
    <AddTodo v-on:add-todo="addTodo" />

    <div v-bind:key="todo.id" v-for="todo in todos">
      <TodoItem v-bind:todo="todo" v-on:del-todo="deleteTodo" />
      <!-- {{ todo.title }} -->
    </div>
  </div>
</template>

<script>
import TodoItem from "./todoItem.vue";
import Header from "./layout/Header.vue";
import AddTodo from "./AddTodo.vue";
import axios from "axios";

export default {
  name: "Todos",
  components: {
    TodoItem,
    Header,
    AddTodo
  },

  data() {
    return {
      todos: []
    };
  },
  methods: {
    deleteTodo(id) {
      this.todos = this.todos.filter(item => item.id !== id);
    },
    addTodo(newTodo) {
      const { title, completed } = newTodo;
      axios
        .post("https://jsonplaceholder.typicode.com/todos", {
          title,
          completed
        })
        .then(res => (this.todos = [...this.todos, res.data]))
        .catch(err => console.log(err));
      this.todos = [...this.todos, newTodo];
    }
  },
  created() {
    axios
      .get("https://jsonplaceholder.typicode.com/todos?_limit=5")
      .then(res => (this.todos = res.data))
      .catch(err => console.log(err));
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
