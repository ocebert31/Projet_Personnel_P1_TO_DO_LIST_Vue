<template>
  <div class="row g-0 text-center bg-custom-gradient vh-100 align-items-center">
    <div class="col-md-5 order-2 order-md-1">
      <div class="m-4 p-4 bg-white rounded box-custom overflow-y-auto" style="max-height: 400px; width: auto;">
        <div class="d-lg-flex flex-row mb-3">
          <h1 class="col p-2 align-self-center fs-4">To Do List</h1>
          <ToDoClear class="col p-2 align-self-center" @tasks-cleared="clearTasks"></ToDoClear>
        </div>
        <div class="d-flex justify-content-left pb-3">
          <ToDoFilter @select-changed="orderTask"></ToDoFilter>
        </div>
        <div class="list-container">
          <draggable v-model="dragList" tag="ul" @start="drag=true" @end="saveOrderChanged" :move="changeOrder" item-key="date">
            <template #item="{element, index}">
              <li :key="index">
                <ToDoTask :task="element" :index="index" @task-updated="updateTask" @task-deleted="deleteTask" @confirmed-edit="confirmEdit"></ToDoTask>
              </li>
            </template>
          </draggable>
        </div>
        <div class="d-flex justify-content-left">
          <ToDoAdd @task-added="addTask"></ToDoAdd>
        </div>
      </div>
    </div>
    <div class="col-md-7 d-flex justify-content-center align-items-center order-1 order-md-2 pt-3">
      <p class="text-white typing-animation">
        To Do List with Vue.js and Bootstrap 
        <br>
        by Bertrand Oceane
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
import draggable from 'vuedraggable';

export default {
  components: {
    ToDoAdd,
    ToDoTask,
    ToDoClear,
    ToDoFilter,
    draggable,
  },

  data() {
    return {
      todoList: [],
      dragList: [],
      drag: false,
      dragIndex: null,
      dragFutureIndex: null,
    };
  },

  created() {
    this.loadList();
  },

  methods: {
    saveList() {
      localStorage.setItem('todoList', JSON.stringify(this.todoList));
      this.dragList = [...this.todoList];
    },

    loadList() {
      const savedList = localStorage.getItem('todoList');
      if (savedList) {
        this.todoList = JSON.parse(savedList).sort((item1, item2) => item1.precedence - item2.precedence);
        this.dragList = [...this.todoList];
      }
    },

    addTask(task) {
      const currentDate = moment().format('YYYY-MM-DD HH:mm:ss.SSS');
      console.log(currentDate)
      this.todoList.push({name: task, isEditing: false, isChecked: false, newName: task, date: currentDate, precedence: this.todoList.length });
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
      if (order === "name") {
        this.orderByNameAsc();
      } else if (order === "date") {
        this.orderByDateDesc();
      } else if (order === "precedence") {
        this.orderByPrecedenceDesc();
      }
    },

    orderByNameAsc() {
      if (this.selected === "name") {
        this.todoList.sort((a, b) => {
          return a.name.localeCompare(b.name);
        });
        this.saveList();
      } 
    },

    orderByDateDesc() {
      if (this.selected === "date") {
        this.todoList.sort((a, b) => {
          return new Date(a.date) - new Date(b.date);
        });
        this.saveList();
      }
    },

    orderByPrecedenceDesc() {
      if (this.selected === "precedence") {
        this.todoList.sort((a, b) => {
          return a.precedence - b.precedence;
        });
        this.saveList();
      }
    },

    changeOrder(event) {
      this.dragIndex = event.draggedContext.index;
      this.dragFutureIndex = event.draggedContext.futureIndex;
    },

    saveOrderChanged() {
      this.drag = false;
      if(this.dragIndex == null || this.dragFutureIndex == null) return true;
      const tasks =  this.todoList.splice(this.dragIndex, 1);
      this.todoList.splice(this.dragFutureIndex, 0, tasks[0]);
      this.todoList.forEach((item, index) => item.precedence = index);
      this.saveList();
      this.dragIndex = null;
      this.dragFutureIndex = null;
      return true;
    },
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

  .list-container > ul {
    list-style-type: none;
    padding-left: 0;
  }

  .task-name {
    word-break: break-all;
  }

  @media (max-width: 576px) {
    .typing-animation {
      font-size: 1.2rem;
    }
  }

  @media (min-width: 576px) {
    .typing-animation {
      font-size:  1.75rem;
    }
  }
</style>
