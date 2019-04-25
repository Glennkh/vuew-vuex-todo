<template>
  <div>
    <h3>Todos</h3>
    <div class="todos">
      <div
        v-bind:class="{'is-complete':todo.completed}"
        @dblclick="onDblClick(todo)"
        v-for="todo in allTodos"
        :key="todo.id"
        class="todo"
      >
        {{todo.title}}
        <span class="deleteButton" @click="deleteTodo(todo.id)">&#10060;</span>
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters, mapActions } from "vuex";
export default {
  name: "Todos",
  computed: mapGetters(["allTodos"]),
  methods: {
    ...mapActions(["fetchTodos", "deleteTodo", "updateTodo"]),
    onDblClick(todo) {
      const updatedTodo = {
        id: todo.id,
        title: todo.title,
        completed: !todo.completed
      };
      this.updateTodo(updatedTodo);
    }
  },
  created() {
    this.fetchTodos();
  }
};
</script>

<style>
.deleteButton {
  cursor: pointer;
}
.is-complete {
  text-decoration: line-through;
}
</style>
