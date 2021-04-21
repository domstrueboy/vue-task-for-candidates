<template>
  <div id="app">
    <h1>{{ icon }} Todo app ({{ counter || '🤷‍♂️'}} items)</h1>
    <form>
      <input type="text" @keydown.enter.prevent="addTodo">
    </form>
    <label>
      <input type="checkbox" v-model="showDone">
      Show done
    </label>
    <ul>
      <li
        v-for="todo in displayedTodos"
        :key="todo.id"
        :class="todo.done ? 'done' : ''"
      >
        <span>{{ todo.text }}</span>
        <button @click="todo.done = !todo.done">✔️</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    icon: {
      type: String,
      default: '🚀',
    }
  },
  data() {
    return {
      input: '',
      showDone: true,
      todos: [
        {
          id: 'id2',
          text: 'Дело №2',
          done: false,
        },
        {
          id: 'id1',
          text: 'Дело №1',
          done: true,
        },
        {
          id: 'id3',
          text: 'Дело №3',
          done: false,
        },
      ]
    };
  },
  computed: {
    counter() {
      return this.todos.filter(todo => !todo.done).length;
    },
    displayedTodos() {
      return this.todos.filter(todo => !todo.done || this.showDone);
    },
  },
  methods: {
    addTodo(e) {
      const text = e.target.value;
      this.todos.push({
        id: `id${Date.now()}`,
        text,
        done: false,
      });
      e.target.value = '';
    }
  },
};
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300&display=swap');
  body {
    font-family: 'Roboto', sans-serif;
    user-select: none;
    display: flex;
    justify-content: center;
  }
  #app {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  input[type="text"] {
    padding: 6px;
    margin-bottom: 6px;
  }
  label {
    padding: 6px;
    background-color: whitesmoke;
    cursor: pointer;
  }
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    margin-bottom: 6px;
  }
  button {
    margin-left: 6px;
    cursor: pointer;
  }
  .done {
    text-decoration: line-through;
    color: lightgray;
  }
</style>
