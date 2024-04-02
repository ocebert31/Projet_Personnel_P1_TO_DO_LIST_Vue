<template>
  <div style="display: flex;" class="col-sm-8 container bg-custom-gradient">
    <div class="container" style="background-color: white; margin: 40px; border-radius: 20px;">
      <h1 class="text-left mb-4">To Do List</h1>
      <ToDoAdd  @task-added="addTask"></ToDoAdd>
      <div class="d-flex gap-3">
        <ToDoFilter @select-changed="orderTask"></ToDoFilter>
        <ToDoClear @tasks-cleared="clearTasks"></ToDoClear>
      </div>
      <ul class="mx-auto" style="padding-left: 0;">
        <li v-for="(item, index) in todoList" :key="index" class="style-liste">
          <ToDoTask :task="item" :index="index"  @task-updated="updateTask" @task-deleted="deleteTask" @confirmed-edit="confirmEdit"></ToDoTask>
        </li>
      </ul>
    </div>
    <div class="col-sm-7 text-center" style="display: flex; justify-content: center; align-items: center;">
      <p style="font-size: 1.5vw; color: white;">
        To Do List with Vue.js and Bootstrap by Bertrand Oceane
      </p>
    </div>
  </div>
</template>

<script>
import ToDoAdd from './ToDoAdd.vue';
import ToDoTask from './ToDoTask.vue';
import ToDoClear from './ToDoClear.vue';
import ToDoFilter from './ToDoFilter.vue';
import moment from 'moment';

export default {
  components: {
    ToDoAdd,
    ToDoTask,
    ToDoClear,
    ToDoFilter,
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
      const currentDate = moment().format('YYYY-MM-DD HH:mm:ss');
      console.log(currentDate)
      this.todoList.push({name: task, isEditing: false, isChecked: false, newName: task, date: currentDate});
      this.saveList();
    },

    deleteTask(index) {
      this.todoList.splice(index, 1);
      this.saveList();
    },

    updateTask(index, task) {
      for (let i = 0; i < this.todoList.length; i++) {
        this.todoList[i].isEditing = false;
      }
      this.todoList[index] = task;
      this.saveList();
    },

    confirmEdit(index, task) {
      this.todoList[index] = task;
      this.saveList();
    },

    clearTasks() {
      localStorage.setItem('todoList', JSON.stringify([]));
      this.loadList();
    },

    orderTask(order) {
      this.selected = order
      if (order === "name-asc") {
        this.orderByNameAsc();
      } else if (order === "name-desc") {
        this.orderByNameDesc();
      } else if (order === "date-desc") {
        this.orderByDateDesc();
      } else if (order === "date-asc") {
        this.orderByDateAsc();
      }
    },

    orderByNameAsc() {
      if (this.selected === "name-asc") {
        this.todoList.sort((a, b) => {
          return a.name.localeCompare(b.name);
        });
        this.saveList();
      } 
    },

    orderByNameDesc() {
      if (this.selected === "name-desc") {
        this.todoList.sort((a, b) => {
          return b.name.localeCompare(a.name);
        });
        this.saveList();
      }
    },

    orderByDateDesc() {
      if (this.selected === "date-desc") {
        this.todoList.sort((a, b) => {
          return new Date(b.date) - new Date(a.date);
        });
        this.saveList();
      }
    },

    orderByDateAsc() {
      if (this.selected === "date-asc") {
      this.todoList.sort((a, b) => {
        return new Date(a.date) - new Date(b.date);
      });
      this.saveList();
      }
    }
  }
};
</script>

<style>
  .style-liste{
    list-style: none;
    display: flex;
  }

  .bg-custom-gradient {
    background: linear-gradient(90deg, #8cc0af, #779c91, #a29a96);
  }
</style>
