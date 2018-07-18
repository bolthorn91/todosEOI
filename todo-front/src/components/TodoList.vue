<template>
  <div id="container">
    <input type="text" v-model="newTodo.text"  @keyup.enter="crearTodo()"> <button @click="crearTodo">Añadir todo</button>

      <ul>
          <li v-for="todo in todos" :key="todo.id">
           El texto es {{todo.text}} y fue creado {{todo.createdAt}}
          </li>

      </ul>




  </div>
</template>

<script>
import axios from "axios"

export default {
  name: "todo-list",
  data() {
    return {
      todos: [],
      newTodo: {
        text: "",
        createdAt: 11,
        iscompleted: true
      }
    };
  },

  methods: {
    recargarTodos() {
      axios.get("http://localhost:2222/api/todos")
        .then(response => (this.todos = response.data));
    },

    crearTodo(){
      axios.post("http://localhost:2222/api/todos", this.newTodo.text)
        .then(response => (this.todos.push(response.data)));
      
    }


  },

  created(){      
    this.recargarTodos(),
    this.crearTodo()
  }


};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
