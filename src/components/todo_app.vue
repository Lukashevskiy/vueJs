<template>
  <div class="container">
    <div class="item">
      <todo_list
      class="float-right"
      v-bind:todos = "todos"
      @deleteToDo="deleteToDo"
      @changeStatusToDo="changeStatusToDo"
      @editToDo="editToDo"
      @create_new_todo="create_new_todo"
      ></todo_list>
    </div>
    <div class="item">
      <todo_edit
      class="float-left"
      v-show="seen"
      v-bind:todo="todo"
      @deleteToDo="deleteToDo"
      @changeStatusToDo="changeStatusToDo"
      @saveChanges="saveChanges"
      ></todo_edit>
    </div>
  </div>
</template>

<script>
import todo_edit from "@/components/todo_edit";
import todo_list from "@/components/todo_list";
export default {
  name: "todo_app",
  components: {todo_list, todo_edit},
  data () {
    return {
      todos: [
        {'id': 0, 'title': 'make a photo', 'description': 'first task', 'checked': true},
        {'id': 1, 'title': 'watch the movie1', 'description': 'second task', 'checked': false},
        {'id': 2, 'title': 'watch the movie2', 'description': 'third task', 'checked': false},
        {'id': 3, 'title': 'watch the movie3', 'description': 'fourth task', 'checked': false},
      ],
      todo: {},
      seen: false,
      id: 4
    }
  },
  methods: {
    deleteToDo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id)
      if (id === this.todo.id) {
        this.seen = false
      }
    },
    changeStatusToDo(id) {
      this.todos.forEach(todo => (todo.id === id ? todo.checked = !todo.checked : ''))
    },
    editToDo(id) {
      this.todos.forEach(todo => (todo.id === id ? this.todo = todo : ''))
      this.seen = true
    },
    saveChanges(data) {
      if (data.id === -1) {
        this.createToDo(data);
      } else {
        this.todos.forEach(todo => {
          if (todo.id === data.id) {
            todo.title = data.title
            todo.description = data.description
          }
        })
        this.seen = false
      }
    },
    createToDo(data) {
      data.id = this.id
      this.id += 1
      let a = JSON.parse(JSON.stringify(data));
      this.todos.push(a)
      console.log(a)
      this.create_new_todo()

    },

    create_new_todo() {
      this.todo = {
        'title': '',
        'description': '',
        'checked': false,
        'id': -1
      }
      this.seen = true
    }

  }
}
</script>

<style scoped>
  .container {
    width: 100%;
    display: flex;
    flex-direction: row;
    justify-content: space-around;
  }

  .item {
    width: 45%;
  }

  .float-left {
    float: left;
  }

  .float-right {
    float: right;
  }



</style>
