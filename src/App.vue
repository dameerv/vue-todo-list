<template>
  <div id="app">
      <h1>Todo application</h1>
    <hr>
    <router-view />
  </div>
</template>

<script>
import Todolist from "./components/Todolist";
import AddTodo from "./components/AddTodo";

export default {
    name: 'App',
    data(){
      return {
          todos:[
              // {id: 1, title: "Купить хлеб", completed: false},
              // {id: 2, title: "Купить масло", completed: false},
              // {id: 3, title: "Купить пиво", completed: false},
          ]
      }
    },
  // mounted() {
  //   fetch('https://jsonplaceholder.typicode.com/todos?_limit=4')
  //     .then(response => response.json())
  //     .then(json => {
  //         this.todos = json
  //     })
  // },
  methods: {
    removeTodo(id){
      this.todos = this.todos.filter(t => t.id !== id)
    },
    addTodo(todo){
      this.todos.push(todo)
    }
  },
  components: {
    Todolist, AddTodo
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
