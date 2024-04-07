<template>
  <div class="row g-0 text-center bg-custom-gradient vh-100 align-items-center">
    <div class="col-6 col-md-4">
      <div class="m-4 p-4 bg-white rounded box-custom">
        <div class="d-flex flex-row mb-3 d-flex justify-content-between">
          <h1 class="p-2 align-self-center fs-2">To Do List</h1>
          <ToDoClear class="p-2 align-self-center" @tasks-cleared="clearTasks"></ToDoClear>
        </div>
        <div class="d-flex justify-content-left pb-3">
          <ToDoFilter @select-changed="orderTask"></ToDoFilter>
        </div>
        <div>
          <ul class="list-unstyled">
            <!-- <draggable v-model="todoList" tag="ul" @start="drag=true" @end="drag=false" :move="changeOrder" item-key="date">
              <template #item="{element, index}">
                <li :key="index">
                  <ToDoTask :task="element" :index="index" @task-updated="updateTask" @task-deleted="deleteTask" @confirmed-edit="confirmEdit"></ToDoTask>
                </li>
              </template>
            </draggable> -->
            <li v-for="(item, index) in todoList" :key="index">
              <ToDoTask :task="item" :index="index" @task-updated="updateTask" @task-deleted="deleteTask" @confirmed-edit="confirmEdit"></ToDoTask>
            </li>
          </ul>
        </div>
        <div class="d-flex justify-content-left">
          <ToDoAdd @task-added="addTask"></ToDoAdd>
        </div>
      </div>
    </div>
    <div class="col-sm-6 col-md-8 d-flex justify-content-center align-items-center">
      <p class="fs-2 text-white typing-animation">
        <span>To Do List with Vue.js and Bootstrap by Bertrand Oceane</span>
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
// import draggable from 'vuedraggable';

export default {
  components: {
    ToDoAdd,
    ToDoTask,
    ToDoClear,
    ToDoFilter,
    // draggable,
  },

  data() {
    return {
      todoList: [],
      drag: false,
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
    },

    // changeOrder(event) {
    //   const tasks =  this.todoList.splice(event.draggedContext.index, 1);
    //   this.todoList.splice(event.draggedContext.futureIndex, 0, tasks[0])
    //   this.saveList();
    // },
  }
};
</script>

<style>
  .bg-custom-gradient {
    background: linear-gradient(90deg, #8cc0af, #779c91, #a29a96);
  }

  .box-custom {
    box-shadow: 0px 0px 15px 5px rgba(255,255,255,0.5);
  }

  @keyframes typing {
  from { width: 0; }
  to { width: 100%; }
  }

  .typing-animation {
    animation: typing 6s steps(60)alternate;
    white-space: nowrap;
    overflow: hidden;
    border-right: 0px solid white;
  }

  ul {
    list-style-type: none;
  }
</style>
