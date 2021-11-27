<template lang="html">
  <div class="card">
    <h5 class="card-title">{{ todo.title }}</h5>
    <div class="card-body">
      <div> Deadline: {{todo.deadline}}</div>
      <div class="text-success" v-if="todo.done">Done</div>
      <div class="text-danger" v-else>To do</div>
      <button v-if="!todo.done" class="btn btn-success float-start btn-sm" v-on:click="deleteTodo(todo)">Done</button>
      <button class="btn btn-danger float-end btn-sm" v-on:click="completeTodo(todo)">X</button>
    </div>

  </div>
</template>

<script lang="js">

  export default  {
    name: 'item',
    props: ['todo'],
    mounted () {

    },
    data () {
      return {

      }
    },
    methods: {
      deleteTodo(todo) {
        this.$emit('complete-todo', todo);
      },
      completeTodo(todo) {
        this.$emit('delete-todo', todo);
      }
    },
    computed: {

    }
}


</script>
