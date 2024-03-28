<template>
    <div>
      <ToDoDelete @task-deleted="deleteTask" :index="index"></ToDoDelete>
      <ToDoChecked :task="task" :index="index" @toggle-task-checked="toggleTaskIsChecked"></ToDoChecked>
      <ToDoName :task="task" :index="index"></ToDoName>
    </div>
</template>
  
<script>
import ToDoChecked from './Task/ToDoIsChecked.vue';
import ToDoName from './Task/ToDoName.vue';
import ToDoDelete from './Task/ToDoDelete.vue';

export default {
  props: ['task', 'index'],

 components: {
  ToDoChecked,
  ToDoName,
  ToDoDelete
 },

 methods: {
  toggleTaskIsChecked() {
    const updatedTask = {name: this.task.name, isChecked: !this.task.isChecked}
    this.$emit('task-updated', this.index, updatedTask);
  },

  deleteTask() {
    this.$emit('task-deleted', this.index);
  }
 }
}
</script>
