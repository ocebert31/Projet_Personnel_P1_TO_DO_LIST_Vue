<template>
    <ul>
      <li v-for="(item, index) in todoList" :key="index" class="style-liste">
        <ToDoDeleteButton @task-deleted="deleteTask" :index="index"></ToDoDeleteButton>
        <ToDoTask :task="item" :index="index"  @task-updated="updateTask"></ToDoTask>
      </li>
    </ul>
    <ToDoInput  @task-added="addTask"></ToDoInput>
</template>

<script>
import ToDoInput from './ToDoAdd.vue';
import ToDoTask from './ToDoTask.vue';
import ToDoDeleteButton from './Task/ToDoDelete.vue';

export default {
  components: {
    ToDoInput,
    ToDoTask,
    ToDoDeleteButton
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
      this.todoList.push({name: task});
      this.saveList();
    },

    deleteTask(index) {
      this.todoList.splice(index, 1);
      this.saveList();
    },

    updateTask(index, task) {
      this.todoList[index] = task;
      this.saveList();
    }
  }
};
</script>

<style>
  .style-liste{
    list-style: none;
    display: flex;
  }
</style>

