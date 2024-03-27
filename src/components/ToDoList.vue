<template>
  <div>
    <ul>
      <li v-for="(item, index) in todoList" :key="index">
        {{ item }}
      </li>
    </ul>
    <ToDoInput  @task-added="addTask"></ToDoInput>
  </div>
</template>

<script>
import ToDoInput from './ToDoInput.vue';

export default {
  components: {
    ToDoInput
  },

  data() {
    return {
      todoList: []
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
    }
  }
};
</script>

<style scoped>
</style>
