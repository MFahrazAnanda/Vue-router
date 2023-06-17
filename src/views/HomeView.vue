<template>
  <div class="container">
    <h1>Selamat Datang</h1>
    <h1>To Do List </h1>
    <div class="add-todo">
      <input v-model="newTodo" placeholder="Tambahkan Kegiatan">
      <button @click="addTodo">Tambah Kegiatan</button>
    </div>
    <div class="filter-todo">
      <button @click="hideCompleted = !hideCompleted">{{ hideCompleted ? 'Tampilkan Semua Kegiatan' : 'Sembunyikan yang sudah selesai' }}</button>
    </div>
    <ul class="todo-list">
      <li v-for="todo in visibleTodos" :key="todo.id">
        <span :class="{ 'completed': todo.completed }" @click="toggleComplete(todo)">{{ todo.text }}</span>
        <div class="todo-buttons">
          <button v-if="!todo.completed" @click="completeTodo(todo.id)">Selesai</button>
          <button v-if="todo.completed" @click="unCompleteTodo(todo.id)">Belum Selesai</button>
          <button @click="removeTodo(todo.id)">Hapus</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      todos: [],
      newTodo: '',
      nextId: 1,
      hideCompleted: false
    }
  },
  computed: {
    visibleTodos() {
      if (this.hideCompleted) {
        return this.todos.filter(todo => !todo.completed);
      } else {
        return this.todos;
      }
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() !== '') {
        this.todos.push({
          id: this.nextId++,
          text: this.newTodo,
          completed: false
        });
        this.newTodo = '';
      }
    },
    removeTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
    },
    completeTodo(id) {
      const todo = this.todos.find(todo => todo.id === id);
      if (todo) {
        todo.completed = true;
      }
    },
    unCompleteTodo(id) {
      const todo = this.todos.find(todo => todo.id === id);
      if (todo) {
        todo.completed = false;
      }
    },
    toggleComplete(todo) {
      todo.completed = !todo.completed;
    }
  }
}
</script>

<style>
.container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
}

h1 {
  font-family: 'comic sans ms';
  font-size: 36px;
  font-weight: bold;
  text-align: center;
}

.add-todo {
  display: flex;
  margin-bottom: 20px;
}

.add-todo input {
  flex-grow: 1;
  padding: 10px;
  font-size: 16px;
  border: 2px solid #ccc;
  border-radius: 5px;
}

.add-todo button {
  margin-left: 10px;
  padding: 10px;
  font-size: 16px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.filter-todo {
  text-align: right;
  margin-bottom: 20px;
}

.filter-todo button {
  padding: 
  10px;
  font-size: 14px;
  background-color: #2196F3;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.todo-list {
  list-style: none;
  padding: 0;
}

li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10px;
  padding: 10px;
  background-color: #f9f9f9;
  border: 1px solid #ddd;
  border-radius: 5px;
}

.completed {
  text-decoration: line-through;
}

.todo-buttons button {
  padding: 5px 10px;
  margin-right: 5px;
  font-size: 14px;
  background-color: #f44336;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

#copyright {
    text-align: center;
    width: 100%;
    padding: 50px 0px 50px 0px;
    margin-top: 50px;
}
</style>