<template>
  <div id="app" class="max-w-2xl mx-auto py-10">
    <h1 class="text-4xl font-bold text-center mb-10">Todo List - Pengumpulan Tugas Sekolah</h1>

    <!-- Form Add Todo -->
    <AddTodo @add-todo="handleAddTodo" />

    <!-- Notifikasi -->
    <Notification v-if="showNotification" :message="notificationMessage" :type="notificationType" />

    <!-- Filter Buttons -->
    <div class="flex justify-center space-x-4 mt-6">
      <button @click="setFilter('all')" :class="{ 'bg-blue-500 text-white': filter === 'all' }"
        class="bg-gray-200 px-4 py-2 rounded-md">
        Semua
      </button>
      <button @click="setFilter('completed')" :class="{ 'bg-blue-500 text-white': filter === 'completed' }"
        class="bg-gray-200 px-4 py-2 rounded-md">
        Selesai
      </button>
      <button @click="setFilter('incomplete')" :class="{ 'bg-blue-500 text-white': filter === 'incomplete' }"
        class="bg-gray-200 px-4 py-2 rounded-md">
        Belum Selesai
      </button>
    </div>

    <!-- List of Todos -->
    <ul class="space-y-4 mt-8">
      <TodoItem v-for="(todo, index) in filteredTodos" :key="index" :todo="todo" @delete-todo="deleteTodo(index)"
        @toggle-complete="toggleComplete(index)" />
    </ul>
  </div>
</template>

<script>
import TodoItem from './components/TodoItem.vue';
import AddTodo from './components/AddTodo.vue';
import Notification from './components/Notification.vue';

export default {
  components: {
    TodoItem,
    AddTodo,
    Notification
  },
  data() {
    return {
      todos: [],
      filter: 'all',
      showNotification: false,
      notificationMessage: '',
      notificationType: ''
    };
  },
  computed: {
    filteredTodos() {
      if (this.filter === 'completed') {
        return this.todos.filter(todo => todo.completed);
      } else if (this.filter === 'incomplete') {
        return this.todos.filter(todo => !todo.completed);
      }
      return this.todos;
    }
  },
  methods: {
    handleAddTodo(todo) {
      if (todo.text) {
        this.todos.push({
          text: todo.text,
          completed: false,
          deadline: todo.deadline
        });
        this.triggerNotification('Tugas berhasil ditambah!', 'success');
      } else {
        this.triggerNotification('Gagal menambahkan tugas. Teks tugas kosong.', 'error');
      }
    },
    deleteTodo(index) {
      this.todos.splice(index, 1);
    },
    toggleComplete(index) {
      this.todos[index].completed = !this.todos[index].completed;
    },
    setFilter(filterType) {
      this.filter = filterType;
    },
    triggerNotification(message, type) {
      this.notificationMessage = message;
      this.notificationType = type;
      this.showNotification = true;
      setTimeout(() => {
        this.showNotification = false;
      }, 3000); // Menghilangkan notifikasi setelah 3 detik
    }
  },
  created() {
    const savedTodos = JSON.parse(localStorage.getItem('todos'));
    if (savedTodos) {
      this.todos = savedTodos;
    }
  },
  watch: {
    todos: {
      handler() {
        localStorage.setItem('todos', JSON.stringify(this.todos));
      },
      deep: true
    }
  }
};
</script>
