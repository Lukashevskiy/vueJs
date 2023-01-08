<template>
<div class="todo-item">
  <div class="left">
   <p>  {{ title }} </p>
  </div>
  <div class="right">
    <input
        class="right_item"
        type="checkbox"
        v-on:click="changeStatusToDo(id)"
        :checked="checked"
    >
    <button class="right_item" v-on:click="editToDo(id)">
      <i class="fa fa-edit"></i>
    </button>
    <button class="right_item" v-on:click="deleteToDO(id)">
      <i class="fa fa-trash"></i>
    </button>
  </div>
</div>
</template>

<script>
export default {
  name: "todo_item",
  data () {
    return {
    }
  },
  props: ['description', 'title', 'id', 'checked'],

  methods: {
    editItem() {
    },
    deleteToDO(id) {
      // console.log(id)
      this.$emit('deleteToDo', id)
    },
    changeStatusToDo(id) {
      this.$emit('changeStatusToDo', id)
    },
    editToDo(id) {
      this.$emit('editToDo', id)
    }
  }
}
</script>

<style scoped>

.todo-item {
  display: flex;
  justify-content: space-between;
  border-top: 2px solid #42b983;
  padding: 2px ;
}

.right_item {
  margin: 3px;
}

.left {
  margin-left: 5px;
  vertical-align: bottom;
}

p {
  margin: 0;
  vertical-align: bottom;
}


input[type="checkbox"] {
  width: 24px;
  height: 24px;
  vertical-align: bottom;
}

</style>
