<template>
    <ul>
      <li v-for="(item, index) in todoList" :key="index" class="style-liste">
        <ToDoTask :task="item" :index="index"></ToDoTask>
      </li>
    </ul>
    <ToDoInput  @task-added="addTask"></ToDoInput>
</template>

<script>
import ToDoInput from './ToDoInput.vue';
import ToDoTask from './ToDoTask.vue';

export default {
  components: {
    ToDoInput,
    ToDoTask
  },

  data() {
    return {
      todoList: [],
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
  }
};
</script>

<style>
  .style-liste{
    list-style: none;
  }
</style>

