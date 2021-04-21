<template>
<!-- Task 1: Implement a counter (line 8), the counter must display a number of active (not done) todos -->
<!-- Task 2: When pressing Enter key in a text input, the page reloads for some reason. Please, fix it -->
<!-- Task 3: Now the page doesn't reload, but nothing happens when pressing Enter key in a text input. Fix it as well -->
<!-- Task 4: The text input persists its value. It should become empty after a Todo added -->
<!-- Task 5: Now the component works as expected. Review it and suggest code style improvements -->
  <div id="app">
    <h1>{{ icon }} Todo app ({{ counter || '🤷‍♂️'}} items)</h1>
    <form>
      <input type="text" @keydown.enter="add_todo">
    </form>
    <label>
      <input type="checkbox" :value="showDone" @change="showDone = !showDone">
      Show done
    </label>
    <ul>
      <li
        v-for="todo in todos"
        v-if="!todo.done || showDone"
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
  methods: {
    add_todo: (e) => {
      const text = e.target.value;
      this.todos.push({
        id: `id${Date.now()}`,
        text,
        done: false,
      });
    }
  },
  created() {
    if (!this.icon) this.icon = '🚀';
  }
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
