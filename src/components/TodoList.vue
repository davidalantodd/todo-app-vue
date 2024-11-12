<script setup lang="ts">
import { ref } from 'vue';

const newTodoText = ref('');
const todos = ref([]);

const addTodo = () => {
  if (newTodoText.value.trim() !== '') {
    todos.value.push({
      text: newTodoText.value,
      completed: false,
    });
    newTodoText.value = '';
  }
};

const removeTodo = (index: number) => {
  todos.value.splice(index, 1);
};


</script>

<template>
  <div>
    <h1>My Todo List</h1>

    <input type="text" v-model="newTodoText" @keyup.enter="addTodo">
    <button @click="addTodo">Add</button>

    <ul>
      <li v-for="(todo, index) in todos" :key="index">
        <input type="checkbox" v-model="todo.completed">
        <span :class="{ completed: todo.completed }">{{ todo.text }}</span>
        <button @click="removeTodo(index)">Remove</button>
      </li>
    </ul>
  </div>
</template>


<style scoped>
.completed {
  text-decoration: line-through;
}
</style>
