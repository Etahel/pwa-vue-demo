<template lang="html">
  <div class="card  w-50 m-auto" style="min-height: 90vh; max-height: 90vh">
    <div class="card-body ">
      <img src="../assets/logo.png" width="50" height="50">
      <h3 class="card-title m-3">PWA To-Do app demo in Vue</h3>
      <h5 class="card-title m-3">Author: Jakub Fornalski</h5>
      <div class="container mt-3 mb-3">
        <div class="row justify-content-center">
          <div class="col-md-auto">
            <form class="m-4">
              <label>Create new task</label>
              <div class="form-group">
                <input class="form-control" id="exampleInputEmail1" v-model="newItem.tile" placeholder="Enter title">
              </div>
              <div class="form-group">
                <date-picker v-model="newItem.deadline" valueType="format"></date-picker>
              </div>
              <button type="button" class="btn btn-primary" v-on:click="addTodo">Add new task</button>
            </form>
          </div>
        </div>
        <div class="row justify-content-center">
          <div class="col-md-auto">
            <div>            Completed Tasks: {{todos.filter(todo => {return todo.done === true}).length}}</div>
          </div>
          <div class="col-md-auto">
            <div>            Pending Tasks: {{todos.filter(todo => {return todo.done === false}).length}}</div>
          </div>
        </div>
      </div>
    <div class=" overflow-auto align-items-center">
    <ul class="overflow-auto list-group align-items-center" style="max-height: 40vh">
      <li v-for="(todo, index) in orderedItems" v-bind:key="index" class="list-group-item"> <item v-on:complete-todo="completeTodo"  v-on:delete-todo="deleteTodo"  v-bind:todo="todo"/> </li>
    </ul>
    </div>
  </div>
  </div>
</template>

<script lang="js">

  import Item from "./Item";
  import _ from 'lodash';
  import DatePicker from 'vue2-datepicker';
  import 'vue2-datepicker/index.css';

  export default  {
    name: 'item-list',
    components: {
      Item,
      DatePicker
    },
    props: [],
    mounted () {

    },
    data () {
      let todosData = JSON.parse(localStorage.getItem('todos'))
      return {
        todos: todosData ? todosData : [],
        newItem: {
          tile:null,
          deadline:null,
          done:false
        }

      };
    },
    methods: {
      deleteTodo(todo) {
        const todoIndex = this.todos.indexOf(todo);
        this.todos.splice(todoIndex, 1);
        console.log(todo)
      },
      completeTodo(todo) {
        this.todos.find(element => _.isEqual(element, todo)).done = true
        // localStorage.setItem('todos', JSON.stringify(this.todos))
      },
      addTodo() {
        let newToDo = {
          title: this.newItem.tile,
          deadline: this.newItem.deadline,
          done: this.newItem.done,
        }
        console.log(newToDo)
        this.todos.push(newToDo)
      },

    },
    computed: {
      orderedItems: function () {
        return _.orderBy(this.todos, 'deadline')
      }
    },
    watch: {
      todos: function () {
        localStorage.setItem('todos', JSON.stringify(this.todos))
      }
    }
}
</script>

