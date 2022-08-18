<template>
  <b-col :col="true" cols="9" class="my-5 mx-auto">
    <b-card>
      <b-col :col="true" cols="12" class="my-5 mx-auto">
      <b-card-body>
        <b-card-title>Simple Todo App With Vue</b-card-title>
          <b-form @submit="addTodo">
            <b-row>
                <b-col :col="true" cols="7">
                  <b-form-input type="text" v-model="todo" @keyup="message = ''" />
                </b-col>
                <b-col :col="true" cols="1">
                  <b-button variant="success" type="submit">ADD</b-button>
                </b-col>
                <b-col :col="true" cols="3">
                  <b-button variant="danger" @click="removeAllTodo">REMOVE ALL TODO</b-button>
                </b-col>
            </b-row>
            <span v-if="message" class="text-danger">{{message}}</span>
          </b-form>
        <small>Total TODO: {{totalTodo}}</small>
        <list-todo-vue :todos="todos" @deleteTodo="deleteTodo" @doneTodo="doneTodo"/>
      </b-card-body>
      </b-col>
      <b-card-footer>By: @Yadi Apriyadi</b-card-footer>
    </b-card>
  </b-col>
</template>

<script>
  import ListTodoVue from './components/ListTodo.vue';

  export default {
    components: {ListTodoVue},
    data() {
      return {
        todo: "",
        message: "",
        todos: []
      }
    },
    mounted() {
      this.todos = JSON.parse(localStorage.getItem('todos'));
    },
    methods: {
      addTodo() {
        if (this.todo === '') {return this.message = 'Please add todo first!'};
        this.todos.push({activity: this.todo, isDone: false});
        this.todo = "";
        this.save();
      },
      deleteTodo(todoIndex) {
        this.todos = this.todos.filter((value, index) => index != todoIndex);
        this.save();
      },
      removeAllTodo() {
        this.todos = [];
        this.save();
      },
      doneTodo(todoIndex) {
        if (this.todos[todoIndex].isDone === true) this.todos[todoIndex].isDone = false;
        else this.todos[todoIndex].isDone = true;
        this.save();
      },
      save() {
        localStorage.setItem('todos', JSON.stringify(this.todos));
      }
    },
    computed: {
      totalTodo() {
        return this.todos.length;
      }
    }
  }
</script>
