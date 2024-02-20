<!-- App.vue -->
<template>
  <div>
    <TodoBoard :todos="todos" @addTodo="addTodo" @deleteTodo="deleteTodo" @editTodo="editTodo" />
  </div>
</template>

<script>
import { ref } from 'vue';
import TodoBoard from './TodoBoard.vue';

export default {
  components: {
    TodoBoard,
  },
  setup() {
    const todos = ref([]);

    const addTodo = (todo) => {
      todos.value.push(todo);
    };

    const deleteTodo = (index) => {
      todos.value.splice(index, 1);
    };

    const editTodo = (index, status) => {
      todos.value[index].completed = status;
    };

    return {
      todos,
      addTodo,
      deleteTodo,
      editTodo,
    };
  },
};
</script>
