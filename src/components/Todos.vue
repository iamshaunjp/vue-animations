<template>
  <div class="todos">
    <input 
      type="text" 
      v-model="newTodo" 
      @keypress.enter="addTodo"
      placeholder="Add a new todo..."
    />
    <div v-if="todos.length">
      <transition-group tag="ul" name="list" appear>
        <li v-for="todo in todos" :key="todo.id" @click="deleteTodo(todo.id)">
          {{ todo.text }}
        </li>
      </transition-group>
    </div>
    <div v-else>Woohoo, nothing left todo!</div>
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  setup(props, { emit }) {
    const todos = ref([
      { text: 'make the bed', id: 1 },
      { text: 'play video games', id: 2 },
    ])
    const newTodo = ref('')

    const addTodo = () => {
      if (newTodo.value) {
        const id = Math.random()
        todos.value = [{ text: newTodo.value, id }, ...todos.value]
        newTodo.value = ''
      } else {
        emit('badValue')
      }
    }

    const deleteTodo = (id) => {
      todos.value = todos.value.filter(todo => todo.id != id)
    }

    return { todos, addTodo, deleteTodo, newTodo }
  }
}
</script>

<style>
  .todos {
    max-width: 400px;
    margin: 20px auto;
    position: relative;
  }
  input {
    width: 100%;
    padding: 12px;
    border: 1px solid #eee;
    border-radius: 10px;
    box-sizing: border-box;
    margin-bottom: 20px;
  }
  .todos ul {
    position: relative;
    padding: 0;
  }
  .todos li {
    list-style-type: none;
    display: block;
    margin-bottom: 10px;
    padding: 10px;
    background: white;
    box-shadow: 1px 3px 5px rgba(0,0,0,0.1);
    border-radius: 10px;
    width: 100%;
    box-sizing: border-box;
  }
  .todos li:hover {
    cursor: pointer;
  }

  /* list transitions */
  .list-enter-from {
    opacity: 0;
    transform: scale(0.6);
  }
  .list-enter-active {
    transition: all 0.4s ease;
  }
  .list-leave-to {
    opacity: 0;
    transform: scale(0.6);
  }
  .list-leave-active {
    transition: all 0.4s ease;
    position: absolute; /* for move transition after item leaves */
  }
  .list-move {
    transition: all 0.3s ease;
  }
</style>