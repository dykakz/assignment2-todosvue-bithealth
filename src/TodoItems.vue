<!-- TodoItems.vue -->
<template>
    <div>
      <ul>
        <li v-for="(todo, index) in todos" :key="index">
          <input type="checkbox" v-model="todo.completed" @change="toggleStatus(index)" />
          <span :class="{ completed: todo.completed }">{{ todo.title }}</span>
          <button @click="deleteItem(index)">Delete</button>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    props: ['todos'],
    methods: {
      deleteItem(index) {
        this.$emit('deleteTodo', index);
      },
      toggleStatus(index) {
        this.$emit('editTodo', index, this.todos[index].completed);
      },
    },
  };
  </script>
  
  <style>
  .completed {
    text-decoration: line-through;
  }
  </style>
  