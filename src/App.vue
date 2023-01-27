<template>
  <div id="app">
    <!-- <Todos v-bind:dataTodos="dataTodos"/> -->
    <AddTodo v-on:add-todo="addTodo" />
  </div>
</template>

<script>
import Todos from './components/Todos.vue'
import AddTodo from './components/AddTodo.vue'

export default {
  name: 'app',
  components:{
    Todos,
    AddTodo,
  },

  //Data Json
  data() {
    return {
      dataTodos: [
        {
          id: 1,
          title: "Go workout",
          completed: false
        },
        {
          id: 2,
          title: "Do laundry",
          completed: false
        },
        {
          id: 3,
          title: "Cook food",
          completed: false
        },
        {
          id: 4,
          title: "Clean up room",
          completed: false
        },
        {
          id: 5,
          title: "Finish work",
          completed: false
        },
      ]
    }
  }
}
</script>

<style>

</style>
