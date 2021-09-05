<template>
  <div id="app" class="container">
    <div class="todoContainer">
      <div class="todoContainer-head">
        <h2>To Do List</h2>
      </div>
      <div class="todoContainer-toDoInput">
        <p>New Todo</p>
        <form id="addToDoForm" @submit.prevent="addTodoItem">
          <input
            id="addToDoValeu"
            name="todoname"
            placeholder="Add to do task..."
            type="text"
            v-model="todoInput"
          />
          <button id="addBtn" type="submit">Add</button>
        </form>
      </div>
      <div id="toDoList" class="todoContainer-toDoList">
        <ul id="items" class="items">
          <div class="item" v-for="(item, index) in items" :key="index">
            <li>{{ item.title }}</li>
            <a href="#" @click.prevent="deleteItem(index)">X</a>
          </div>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
const localKey = "todos";

export default {
  name: "App",
  data() {
    return {
      todoInput: "",
      items: [],
    };
  },
  methods: {
    addTodoItem() {
      if (this.todoInput == "") {
        return;
      }
      this.items.push({
        title: this.todoInput,
      });
      this.todoInput = "";
    },
    deleteItem(index) {
      this.items.splice(index, 1);
    },
  },
  mounted() {
    const items = localStorage.getItem(localKey) || "[]";
    this.items = JSON.parse(items);
  },
  watch: {
    items: {
      deep: true,
      handler(items) {
        localStorage.setItem(localKey, JSON.stringify(items));
      },
    },
  },
};
</script>
