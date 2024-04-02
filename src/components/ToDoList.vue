<template>
  <div style="display: flex; gap: 30px">
    <ToDoFilter @select-changed="orderTask"></ToDoFilter>
    <ToDoClear @tasks-cleared="clearTasks"></ToDoClear>
  </div>
    <ul>
      <li v-for="(item, index) in todoList" :key="index" class="style-liste">
        <ToDoTask :task="item" :index="index"  @task-updated="updateTask" @task-deleted="deleteTask" @confirmed-edit="confirmEdit"></ToDoTask>
      </li>
    </ul>
    <ToDoAdd  @task-added="addTask"></ToDoAdd>
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
      localStorage.removeItem('todoList');
      this.todoList = [];
      this.saveList();
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
</style>

