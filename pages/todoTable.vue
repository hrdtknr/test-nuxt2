<template>
  <v-data-table
    :headers="headers"
    :items="todoList"
    :items-per-page="5"
    class="elevation-1"
  ></v-data-table>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      updName: "",
      updTodo: "",
      headers: [
        {
          text: "ID",
          align: "start",
          sortable: false,
          value: "id"
        },
        { text: "NAME", value: "name" },
        { text: "TODO", value: "todo" }
      ],
      todoList: [
        {
          id: null,
          name: null,
          todo: null
        }
      ]
    };
  },
  mounted() {
    axios
      .get("http://localhost:8000/todoList")
      .then(response => (this.todoList = response.data))
      .catch(error => console.log(error));
  },
  methods: {
    getTodo: function() {
      axios
        .get("http://localhost:8000/todoList")
        .then(response => (this.todoList = response.data))
        .catch(error => console.log(error));
    },
    updateTodo: function(todo) {
      axios
        .put("http://localhost:8000/todoList", {
          id: todo.id,
          name: todo.name,
          todo: todo.todo
        })
        .catch(error => console.log(error));
    },
    deleteTodo: function(delId) {
      const params = { id: delId };
      const qs = new URLSearchParams(params);
      axios
        .delete(`http://localhost:8000/todoList?${qs}`)
        .then(() => this.getTodo())
        .catch(error => console.log(error));
    }
  }
};
</script>
<style scoped>
.table {
  background-color: aqua;
  padding: 10px;
  margin: 10px;
}
</style>
