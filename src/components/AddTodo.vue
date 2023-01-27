<template>
  <div>

    <!-- Form input -->
    <InputForm 
      @submitEdit="editProcess" 
      @submitForm="addTodo"
      v-bind:todo="todo"
      v-bind:todos="todos"
      v-bind:editForm="editForm"
      v-bind:editTodo="editTodo" 
    />



    <table border="1" style="margin-top: 30px">
      <tr>
        <td>Title</td>
        <td>due date</td>
        <td>status</td>
        <td>action</td>
      </tr>

      <!-- lakukan perulangan (v-for) kemudian masukkan value (record), key(index) di dalam state todos -->
      <tr v-for="(record, index) in todos">
          <td v-if="record.status === 'Incomplete' ">
            <strike >
            {{ index }} {{ record.title }}
            </strike>
          </td>
          <td v-else> 
              {{ index }} {{ record.title }}
          </td>


          <td :class="dateClass(record)">{{ record.duedate }}</td>
          <!-- <td :class="dateClass"  >{{ record.duedate }}</td> -->
          <td>{{ record.status }}</td>


          <td>
            <a href="#" @click.prevent="showEditForm(index)">Edit</a> | 
            <a href="#" @click.prevent="openDialog = true">Delete</a>
          </td>
      </tr>
    </table>

    <Dialogs 
      v-if="openDialog"
      @cancel="onCancel" 
      @confirm="onConfirm"
      text="Apakah Yakin untuk Menghapus Item ini ?" 
    />



  </div>
</template>

<script>
// import uuid from 'uuid';

import Dialogs from './Dialogs/index.vue'
import InputForm from './FormTodo/InputForm.vue'

export default {
  name: "addTodo",
  components: {
    Dialogs,
    InputForm,
  },

  data(){
    return {
      todo: {
        title: '',
        duedate: '',
        status: '',
      },
      editTodo: null,
      editForm: false,
      editIndex: null,
      todos: [],
      openDialog: false,
    }
  },
  

  methods: {

    dateClass(todo) {

      let today = new Date()
      let date = new Date(todo.duedate)

      return {
        'red': date < today,
        'yellow': date && today,
        'green': date > today
      }

    },

    onCancel() {
      this.openDialog = false // <==== state openDialog ubah jadi false untuk modal tutup ketika klik batal
    },

    onConfirm() {
      this.openDialog = false // <==== state openDialog ubah jadi false untuk modal tutup setelah di confirm
      Object.entries(this.todos.splice(this.todos,1)) // <==== ketika di console data ini object convert data ini jadi array kemudian update element atau delete array
    },

    editProcess() {
      this.todos[this.editIndex] = this.editTodo
      this.editIndex = null
      this.editForm = false
    }, 


    //proses show edit
    showEditForm(index) {
      this.editTodo = JSON.parse(JSON.stringify(this.todos[index]))
      this.editIndex = index
      this.editForm = true
    },

    addTodo(e){
      e.preventDefault();

      const newTodoObj = {
        id: Math.random(),
        title: this.todo.title,
        duedate: this.todo.duedate,
        status: this.todo.status
      }

      // this.$emit('add-todo', newTodoObj);

      /**
       * add actual todo to body
       */
      this.todos.push(newTodoObj)

      /**
       * clear form
       */
      this.todo.title = '';
      this.todo.duedate = '';

    }
  }
}

</script>

<style>
.yellow {
  color: yellow;
}

.green {
  color: green;
}

.red {
  color: red;
}
</style>