<template>
  <b-list-group class="w-50 mt-3">
    <b-list-group-item v-for="(todo, index) in todos" :key="index">
      <b-row>
        <b-col :col="true">
          <span class="fs-5" v-if="todo.isDone">
            <del>{{todo.activity}}</del>
          </span>
          <span v-else>{{todo.activity}}</span>
        </b-col>
        <b-col :col="true" cols="auto">
          <b-button variant="info" @click="done(index)">DONE</b-button>
        </b-col>
        <b-col :col="true" cols="auto">
          <b-button variant="danger" @click="deleteTODO(index)">X</b-button>
        </b-col>
      </b-row>
    </b-list-group-item>
  </b-list-group>
</template>

<script>
  export default {
    props: {
      todos: {
        type: Array,
        default: [],
        required: true,
        validator(value) {
          return value.length === 0;
        }
      }
    },
    methods: {
      deleteTODO(todoId) {
        this.$emit('deleteTodo', todoId);
      },
      done(index) {
        this.$emit('doneTodo', index);
      },
    }
  }
</script>