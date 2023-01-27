<template>
  <div>
    <h2>My todolist</h2>
    <ul>
      <li v-bind:key="todo.id" v-for="todo in dataTodos">
        <Todo v-bind:todo="todo" />
      </li>
    </ul>
  </div>
</template>

<script>
import Todo from './Todo.vue';
export default {
  name: 'Todos',
  components: {
    Todo
  },
  props: [
    "dataTodos"
  ]
}
</script>