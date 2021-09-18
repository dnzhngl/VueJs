<template>
  <div class="container">
    <div class="row">
      <div class="col-md-8 offset-md-3 text-center">
        <h3 class="mt-5">Todo List | Vue.js</h3>
        <hr />
        <div class="row">
          <div
            class="col-md-6 offset-md-3 d-flex flex-row justify-content-between align-items-center p-2 "
          >
              <input type="text" v-model="todoText" />
              <button @click="addTodo()" class="btn btn-primary">Add</button>
          </div>
        </div>
        <hr>
        <div class="todo-container">
          <Todo @deleteTodo="deleteTodo($event)" v-for="todo in todoList" :todo="todo" :key="todo.id"/>
        </div>
      </div>
    </div>
    <!-- <button @click="fetchTodos">Feth Todos</button> -->
  </div>
</template>

<script>
import Todo from "@/components/Todo"
import axios from "axios"
export default {
  name: "App",
  components: {
    Todo
    },
    data(){
      return{
        todoText : "",
        todoList : []
      }
    },
    methods : {
      addTodo(){
        axios.post("https://vuejs-1-videoda-default-rtdb.firebaseio.com/todoList.json", { text : this.todoText })
        .then(response => {
          console.log(response)
          this.todoList.push({
            id : response.data.name,
            text : this.todoText
          })
        })
        .catch( error => {
          console.log(error)
        })
      },
      deleteTodo(todoId){
        axios.delete("https://vuejs-1-videoda-default-rtdb.firebaseio.com/todoList/" + todoId + ".json")
        .then(response => {
          console.log(response)
          let index = this.todoList.findIndex(t => {
            return t.id == todoId
          })
          console.log(index)

          this.todoList.splice(index,1)

        })
        .catch(error => {
          console.log(error)
        })
      }
    }, 
    created(){
        axios.get("https://vuejs-1-videoda-default-rtdb.firebaseio.com/todoList.json")
        .then(response => {
          console.log(response.data)
          for(let key in response.data){
            console.log(response.data[key])
            let todo = {
              text : response.data[key].text,
              id : key
            }
            this.todoList.push(todo)
          }
        })
        .catch(error => {
          console.log(error)
        })
      }
};
</script>