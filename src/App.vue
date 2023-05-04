
<template>
  <div>
    <form @submit.prevent = "addTodo" >
      <input type="text" placeholder="type todo..." v-model="todo" />
      <button type="submit" :disabled = !todo >Add</button>
    </form>
    <div class="todo" v-for="todo in todos" :key=todo.id :class="{'done' : todo.done}">
      <h3> {{todo.content}} </h3>
      <div class="btns">
        <button @click = "doneTodo(todo.id)" >Done</button>
        <button @click = "deleteTodo(todo.id)" >Remove</button>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import { v4 as uuidv4 } from 'uuid';

export default {
  name: 'App',
  setup() {
    const todos = ref([])
    const todo = ref('')

    const addTodo = (e) => {
      e.preventDefault();
      const newTodo = {
        id: uuidv4(),
        content: todo.value,
        done: false
      }
      todo.value = ''
      todos.value.unshift(newTodo)
    }

    const deleteTodo = (id) => {
      todos.value = todos.value.filter((todo) => todo.id !== id)
    }

    const doneTodo = (id, done) => {
      const index = todos.value.findIndex(todo => todo.id === id)
      todos.value[index].done = !todos.value[index].done
    }

    return {
      todos,
      todo,
      addTodo,
      deleteTodo,
      doneTodo
    }
  }
}

</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;500;600;700;800;900&family=Poppins:wght@100;200;300;400;500;600;700;800;900&display=swap');

  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Poppins' sans-serif;
  }

  body {
    display: flex;
    align-items: center;
    justify-content: center;
  }

  #app {
    max-width: 500px;
    width: 100%;
    margin: 5rem 1rem;
  }

  form {
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0.5rem 1rem;
    padding-right: 0.5rem;
    background-color: #c9c9c9;
    margin-bottom: 3rem; 
    border-radius: 0.5rem;
  }

  form input {
    padding: 0.5rem 1rem;
    border: none;
    background: none;
  }
  form input:focus {
    outline: none;
    background: none;
  }

  form button {
    padding: 0.5rem 1rem;
    border-radius: 0.5rem;
    border: none;
    background-color: #001755;
    color: #ffffff;

  }

  button {
    cursor: pointer;
    transition: 0.4s;
  }

  .todo {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem;
    margin: 0.5rem 0;
    border-radius: 0.5rem;
    background-color: #dddddd;
    transition: 0.4s;
    font-family: 'Poppins';
  }
  .done {
    background-color: #71ff88;
    text-decoration: line-through;
  }

  .btns button {
    padding: 0.5rem 1rem;
    border-radius: 0.5rem;
    border: none;
  }
  .btns button:nth-child(1) {
    background-color: #1b5500;
    margin-right: 1rem;
    color: #ffffff;
  }
  .btns button:nth-child(2) {
    background-color: #ac0000;
    color: #ffffff;
  }
</style>
