<template>
  <div class="max-w-md mx-auto mt-10 p-6 bg-red-200 border-4 border-black">
    <h1 class="text-3xl font-extrabold uppercase mb-4 text-center border-b-4 border-black pb-2">
      Todo List
    </h1>
    <div class="flex mb-4">
      <input
        v-model="newTodo"
        @keyup.enter="addTodo"
        placeholder="Add a new todo..."
        class="flex-grow border-4 border-black p-2 bg-white"
      />
      <button
        @click="addTodo"
        class="bg-black text-white font-bold p-2 border-4 border-black hover:bg-white hover:text-black transition-colors"
      >
        Add
      </button>
    </div>
    <ul>
      <li
        v-for="(todo, index) in todos"
        :key="index"
        class="flex items-center justify-between py-2 border-b-4 border-black"
      >
        <div class="flex items-center space-x-2">
          <input
            type="checkbox"
            v-model="todo.completed"
            class="w-5 h-5 border-4 border-black"
          />
          <span :class="{ 'line-through opacity-50': todo.completed }" class="font-bold">
            {{ todo.text }}
          </span>
        </div>
        <button
          @click="removeTodo(index)"
          class="bg-red-500 text-white font-bold px-2 py-1 border-4 border-black hover:bg-red-700 transition-colors"
        >
          Remove
        </button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'TodoPage',
  data() {
    return {
      newTodo: '',
      todos: [
        { text: 'Learn Vue.js', completed: false },
        { text: 'Build a Todo App', completed: false },
        { text: 'Read a book', completed: false }
      ]
    };
  },
  methods: {
    addTodo() {
      const trimmedText = this.newTodo.trim();
      if (trimmedText) {
        this.todos.push({ text: trimmedText, completed: false });
        this.newTodo = '';
      }
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    }
  }
};
</script>