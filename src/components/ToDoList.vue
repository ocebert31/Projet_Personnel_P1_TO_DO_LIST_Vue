<template>
    <ul>
      <li v-for="(item, index) in todoList" :key="index">
        <input type="checkbox" :id="'checkbox-' + index" v-model="isChecked" />
        <label for="checkbox" :class="{ 'styled': isChecked }">{{ item }}</label>
      </li>
    </ul>
    <ToDoInput  @task-added="addTask"></ToDoInput>
</template>

<script>
import ToDoInput from './ToDoInput.vue';

export default {
  components: {
    ToDoInput
  },

  data() {
    return {
      todoList: [],
      isChecked: false
    };
  },

  created() {
    this.loadList();
  },

  methods: {
    saveList() {
      localStorage.setItem('todoList', JSON.stringify(this.todoList));
    },

    loadList() {
      const savedList = localStorage.getItem('todoList');
      if (savedList) {
        this.todoList = JSON.parse(savedList);
      }
    },

    addTask(task) {
      this.todoList.push(task);
      this.saveList();
      this.loadList();
    },

    toggleTask(task) {
      task.clicked = !task.clicked;
    }
  }
};
</script>



<style scoped>
  .styled {
    text-decoration: line-through;
  }
</style>
