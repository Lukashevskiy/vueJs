<template>
  <div class="todo_list_container ">
    <div class="todo_list_header">
      <button class="add-button" v-on:click="$emit('create_new_todo')">add</button>
    </div>
    <div>
      <div class="todo_list_content">
      <todo_item v-for="todo in todos"
          :key="todo.id"
          v-bind:title="todo.title"
          v-bind:description="todo.description"
          v-bind:checked="todo.checked"
          v-bind:id="todo.id"
        @deleteToDo="$emit('deleteToDo', todo.id)"
        @changeStatusToDo="$emit('changeStatusToDo', todo.id)"
        @editToDo="$emit('editToDo', todo.id)"
        > </todo_item>
      </div>
    </div>
  </div>
</template>

<script>
import todo_item from "@/components/todo_item";
export default {
  name: "todo_list",
  components: {todo_item},
  data() {
    return {}
  },
  methods: {
    create_todo(){}
  },
  props: ['todos'],
  emits: ['deleteToDo', 'checkToDo', 'editToDo']
}
</script>

<style scoped>
.todo_list_container {
  display: flex;
  flex-direction: column;
  border: 2px solid #42b983;
  width: 470px;
  padding: 15px 0 10px 0;
  box-sizing: border-box;
}

.add-button {
  float: left;
  border: 1px solid #42b983;
  width: 80px;
  height: 30px;
  margin: 0 auto 5px 10px;
}

</style>
