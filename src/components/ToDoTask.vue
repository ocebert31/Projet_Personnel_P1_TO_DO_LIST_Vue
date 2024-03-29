<template>
  <div class="alignement">
    <ToDoEdit @edit-mode-toggled="toggleEditMode"></ToDoEdit>
    <ToDoDelete @task-deleted="deleteTask" :index="index"></ToDoDelete>
    <ToDoChecked :task="task" :index="index" @toggle-task-checked="toggleTaskIsChecked"></ToDoChecked>
    <ToDoName :task="task" :index="index" :isEditing="isEditing"></ToDoName>
  </div>
</template>

<script>
import ToDoChecked from './Task/ToDoIsChecked.vue';
import ToDoName from './Task/ToDoName.vue';
import ToDoDelete from './Task/ToDoDelete.vue';
import ToDoEdit from './Task/ToDoEdit.vue';

export default {
  props: ['task', 'index'],

 components: {
  ToDoChecked,
  ToDoName,
  ToDoDelete,
  ToDoEdit
 },

 data() {
    return {
      message: '',
      isEditing: false // Ajout de la variable isEditing pour suivre l'état d'édition
    };
  },

 methods: {
  toggleTaskIsChecked() {
    const updatedTask = {name: this.task.name, isChecked: !this.task.isChecked}
    this.$emit('task-updated', this.index, updatedTask);
  },

  deleteTask() {
    this.$emit('task-deleted', this.index);
  },

  toggleEditMode() {
    this.isEditing = !this.isEditing;
  },
 }
}
</script>