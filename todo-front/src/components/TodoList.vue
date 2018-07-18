<template>
  <div id="container">
    <input type="text" v-model="newTodo.text" v-on:keyup.enter="crearTodo"> 
    <button @click="crearTodo">Añadir todo</button>

      <ul>
          <li v-for="todo in todos" :key="todo.id">
           El texto es {{todo.text}} y fue creado {{todo.createdAt}}
          <button @click="editarTodo" v-bind="todo.id">Editar todo</button>
          <button @click="borrarTodo" v-bind="todo.id">Borrar todo</button>

          </li>

      </ul>




  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "todo-list",

  data() {
    return {
      todos: [],
      newTodo: {
        text: "",
        createdAt: 11,
        isCompleted: true
      }
    };
  },

  methods: {
    recargarTodos() {
      axios
        .get("http://localhost:2222/api/todos")
        .then(response => (this.todos = response.data));
    },

    crearTodo() {
      axios.post("http://localhost:2222/api/todos", this.newTodo)
        .then(response => this.todos.push(response.data));

      },
        
    editarTodo(){
      axios.patch("http://localhost:2222/api/todos/"+this.todo.id, this.newTodo.text)
      .then(response => this.todos.findIndex(idx => idx.id === response.data.id))
      
    },

    borrarTodo(){
      axios.delete("http://localhost:2222/api/todos/"+this.todo.id, this.newTodo.text)      
    }
  },
  

  created() {
    this.recargarTodos()
  },


  computed: {
    totalPrice() {
      let result = 0;
      this.items.forEach(item => (result += item.price));
      return result;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
