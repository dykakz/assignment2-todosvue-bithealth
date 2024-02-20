<!-- TodoBoard.vue -->
<template>
  <div class="todo-board">
    <h2>Add Todo</h2>
    <div class="add-todo">
      <input type="text" v-model="newTodo" placeholder="Enter your todo..." />
      <button @click="addNewTodo">Add</button>
    </div>

    <h2>Todo List</h2>
    <TodoItems :todos="todos" @deleteTodo="deleteTodo" @editTodo="editTodo" />
  </div>
</template>

<script>
import { ref } from 'vue';
import TodoItems from './TodoItems.vue';

export default {
  components: {
    TodoItems,
  },
  props: ['todos'],
  setup(props, { emit }) {
    const newTodo = ref('');

    const addNewTodo = () => {
      if (newTodo.value.trim() !== '') {
        emit('addTodo', { title: newTodo.value, completed: false });
        newTodo.value = '';
      }
    };

    const deleteTodo = (index) => {
      emit('deleteTodo', index);
    };

    const editTodo = (index, status) => {
      emit('editTodo', index, status);
    };

    return {
      newTodo,
      addNewTodo,
      deleteTodo,
      editTodo,
    };
  },
};
</script>

<style scoped>
.todo-board {
  max-width: 400px;
  margin: 0 auto;
}

.add-todo {
  display: flex;
  margin-bottom: 20px;
}

.add-todo input[type="text"] {
  flex: 1;
  padding: 8px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.add-todo button {
  padding: 8px 16px;
  font-size: 16px;
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.add-todo button:hover {
  background-color: #45a049;
}

h2 {
  font-size: 20px;
  margin-top: 30px;
  margin-bottom: 10px;
}
</style>
