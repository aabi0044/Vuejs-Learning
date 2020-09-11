<template>
  <div class="hello">
 <Header/>

    <div v-bind:key="todo.id" v-for="todo in todos">
        <TodoItem v-bind:todo="todo" v-on:del-todo="deleteTodo" />
      <!-- {{ todo.title }} -->
    </div>
  </div>
</template>

<script>

import TodoItem from './todoItem.vue';
import Header from './layout/Header.vue';

export default {
  name: "Todos",
  components:{
      TodoItem,
      Header
  },

  data() {
    return {
      todos: [
        {
          id: 1,
          title: "Todo One",
          completed: false
        },
        {
          id: 2,
          title: "Todo two",
          completed: true
        },
        {
          id: 3,
          title: "Todo three",
          completed: false
        }
      ]
    };
  },
  methods:{
      deleteTodo(id){
          this.todos = this.todos.filter(item=>item.id!==id);
      }
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
