<script setup>
import { ref, computed, watch } from 'vue'

// State
const todos = ref(JSON.parse(localStorage.getItem('todos')) || [])
const newTodo = ref('')
const filter = ref('all')

// Add Todo
const addTodo = () => {
  if (!newTodo.value.trim()) return
  todos.value.push({
    id: Date.now(),
    text: newTodo.value,
    completed: false
  })
  newTodo.value = ''
}

// Remove Todo
const removeTodo = (id) => {
  todos.value = todos.value.filter(t => t.id !== id)
}

// Toggle Complete
const toggleTodo = (id) => {
  const todo = todos.value.find(t => t.id === id)
  if (todo) todo.completed = !todo.completed
}

// Filter Todos
const filteredTodos = computed(() => {
  if (filter.value === 'completed') {
    return todos.value.filter(t => t.completed)
  }
  if (filter.value === 'pending') {
    return todos.value.filter(t => !t.completed)
  }
  return todos.value
})

// Save to localStorage
watch(todos, (val) => {
  localStorage.setItem('todos', JSON.stringify(val))
}, { deep: true })
</script>

<template>
  <div class="app">
    <h1>📝 Vue To-Do App</h1>

    <!-- Input -->
    <div class="input-box">
      <input 
        v-model="newTodo" 
        @keyup.enter="addTodo"
        placeholder="Add a task..." 
      />
      <button @click="addTodo">Add</button>
    </div>

    <!-- Filters -->
    <div class="filters">
      <button @click="filter='all'" :class="{active: filter==='all'}">All</button>
      <button @click="filter='completed'" :class="{active: filter==='completed'}">Completed</button>
      <button @click="filter='pending'" :class="{active: filter==='pending'}">Pending</button>
    </div>

    <!-- List -->
    <ul>
      <li v-for="todo in filteredTodos" :key="todo.id">
        <input 
          type="checkbox" 
          :checked="todo.completed"
          @change="toggleTodo(todo.id)"
        />

        <span :class="{done: todo.completed}">
          {{ todo.text }}
        </span>

        <button @click="removeTodo(todo.id)">❌</button>
      </li>
    </ul>
  </div>
</template>

<style>
.app {
  max-width: 400px;
  margin: 40px auto;
  font-family: Arial, sans-serif;
  text-align: center;
}

.input-box input {
  padding: 8px;
  width: 65%;
}

.input-box button {
  padding: 8px;
  margin-left: 5px;
}

.filters {
  margin: 15px 0;
}

.filters button {
  margin: 0 5px;
  padding: 5px 10px;
}

.filters .active {
  background-color: #42b983;
  color: white;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 8px 0;
}

.done {
  text-decoration: line-through;
  color: gray;
}
</style>