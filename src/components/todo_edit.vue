<template>
  <div class="todo_edit_container">
    <div class="todo_edit_header">
      <h3 class="todo_edit_title">
        <input type="text" v-model="cur_todo.title">
      </h3>
      checked: {{cur_todo.checked}}
    </div>

    <div class="todo_edit_content">
      <textarea class="todo_edit_content_input" type="text" v-model="cur_todo.description"> </textarea>

    </div>

    <div class="todo_edit_buttons">
      <button class="todo-edit-button" v-on:click="saveChanges">save</button>
      <button class="todo-edit-button" v-on:click="changeStatus(cur_todo.id)">{{check_message}}</button>
      <button class="todo-edit-button" v-on:click="deleteToDo(cur_todo.id)">delete</button>
    <!-- save, check, delete-->
    </div>
  </div>
</template>

<script>
export default {
  name: "todo_edit",
  data() {
    return {
      cur_todo: {
        title: '',
        description: '',
        checked: false,
        id: ''
      }
    }
  },
  computed: {
    check_message: function () {
      return this.checked ? 'start' : 'finish'
    }
  },
  methods: {
    changeStatus(id) {
      this.checked = ! this.checked
      this.$emit('changeStatusToDo', id)
    },
    deleteToDo(id) {
      this.$emit('deleteToDo', id)
    },
    saveChanges() {
      console.log(this.cur_todo.description)
      // console.log('todo_edit.vue', this.cur_todo)
      this.$emit('saveChanges', this.cur_todo)
    }
  },
  props: ['todo'],
  watch: {
    todo: function () {
      this.cur_todo.title = this.todo.title
      this.cur_todo.id = this.todo.id
      this.cur_todo.description = this.todo.description
      this.cur_todo.checked = this.todo.checked
    },

  }
}
</script>

<style scoped>

.todo_edit_container {
  display: flex;
  flex-direction: column;
  border-bottom: none;
  width: 450px;
  padding: 0 0 0 0;

}

.todo_edit_header {
  border: 2px solid #42b983;
  border-bottom: none;
}

.todo_edit_title {
  text-align: left;
  padding-left: 12px;
}

.todo_edit_content  {
  border: 2px solid #42b983;

}

.todo_edit_content_input {
  margin: 8px;
  width: 420px;
  resize: none;
  height: 300px;
  border: 1px solid darkseagreen;
}

.todo_edit_buttons {
  padding-bottom: 10px;
}

.todo-edit-button {
  border-top: 1px solid #42b983;
  border-bottom: 2px solid #42b983;
  width: 150px;
  height: 50px;
  cursor: pointer;
}

.todo_edit_buttons .todo-edit-button:first-child {
  border-left: 2px solid #42b983;
}

.todo_edit_buttons .todo-edit-button:last-child {
  border-right: 2px solid #42b983;
}

div {
  box-sizing: border-box;
}
</style>
