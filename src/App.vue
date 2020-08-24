<template>
  <div id="app">
    <headerview/>
    <addtodo v-on:add-todo="addTodo"/>
    <todo v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import headerview from './components/layouts/headerview'
import todo from './components/todo'
import addtodo from './components/addtodo'
import axios from 'axios'
export default {
  name: 'App',
  components: {
    headerview,
    todo,
    addtodo
  },
  data(){
    return {
      todos:[]
    }
  },
  methods:{
    addTodo(newtodo)
    {
      const {title,completed} = newtodo;
      axios.post('https://jsonplaceholder.typicode.com/todos',{
        title,
        completed
      })
      .then(res => this.todos = [...this.todos,res.data])
      .catch(err => console.log(err))
    },
    deleteTodo(id){
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then(res => {
        this.todos = this.todos.filter((todo) => todo.id !== id)
        console.log(res.data);
        })
      .catch(err => console.log(err))
    }
  },
  created(){
      axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
      .then(res => this.todos = res.data)
      .catch(err => console.log(err))
    }
}
</script>

<style>
*{
  box-sizing:border-box;
  margin:0;
  padding:0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
