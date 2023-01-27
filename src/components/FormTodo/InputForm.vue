<template>
  <div>
    <h1>Todo List</h1>
    <form @submit.prevent="submitForm" v-if="!editForm">
      <input type="text" v-model="todo.title"  name="title">
      <input type="date" v-model="todo.duedate"  />
      <select type="select" v-model="todo.status"  >
        <option>
          Incomplete
        </option>
        <option>
          complete
        </option>
      </select>
      <button type="submit">add</button>
    </form>
    <form @submit.prevent="submitEdit" v-if="editForm">
      <input type="text" v-model="editTodo.title" name="title">
      <input type="date" v-model="editTodo.duedate" />
      <select type="select" v-model="editTodo.status">
        <option>
          Incomplete
        </option>
        <option>
          complete
        </option>
      </select>
      <button type="submit">close</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "InputForm",
  props: [
    "todo",
    "todos",
    "editForm",
    "editTodo",
  ],
  
  methods: {

    submitForm(todos){
      this.$emit('submitForm', todos)
    },

    submitEdit(editTodo){
      this.$emit('submitEdit', editTodo)
    }

    
  }
}
</script>