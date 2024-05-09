<template>
  <div id="app">
    <h1>Vue To-Do List</h1>

    <div class="input-container">
      <input type="text" v-model="newItem" placeholder="Add new item">
      <button @click="addItem">Add</button>
    </div>

    <transition-group name="fade" tag="ul" class="todo-list">
      <li v-for="(item, index) in items" :key="index" class="todo-item">
        <span>{{ item }}</span>
        <div class="button-container">
          <button @click="editItem(index)">Edit</button>
          <button @click="deleteItem(index)">Delete</button>
        </div>
      </li>
    </transition-group>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newItem: '',
      items: []
    };
  },
  methods: {
    addItem() {
      if (this.newItem !== '') {
        this.items.push(this.newItem);
        this.newItem = '';
      }
    },
    editItem(index) {
      const updatedItem = prompt('Update item:', this.items[index]);
      if (updatedItem !== null) {
        this.items.splice(index, 1, updatedItem);
      }
    },
    deleteItem(index) {
      if (confirm('Are you sure you want to delete this item?')) {
        this.items.splice(index, 1);
      }
    }
  }
};
</script>

<style scoped>
#app {
  max-width: 500px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
}

.input-container {
  margin-bottom: 20px;
}

.input-container input {
  padding: 8px;
  width: 60%;
  border-radius: 4px;
  border: 1px solid #ccc;
}

.input-container button {
  padding: 8px 12px;
  border: none;
  background-color: #007bff;
  color: #fff;
  border-radius: 4px;
  cursor: pointer;
}

.todo-list {
  list-style: none;
  padding: 0;
}

.todo-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px;
  border-bottom: 1px solid #ccc;
}

.todo-item:last-child {
  border-bottom: none;
}

.button-container button {
  padding: 6px 10px;
  margin-left: 10px;
  border: none;
  background-color: #dc3545;
  color: #fff;
  border-radius: 4px;
  cursor: pointer;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s;
}

.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>