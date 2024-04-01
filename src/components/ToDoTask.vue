<template>
  <div class="alignement">
    <ToDoChecked :task="task" :index="index" @toggle-task-checked="toggleTaskIsChecked"></ToDoChecked>
    <ToDoName :task="task" @name-changed="changeName"></ToDoName>
    <div v-if="!task.isEditing" style="display: flex;">
      <ToDoEdit @edit-mode-toggled="toggleTaskIsEditing" class="style-bouton-mode-normal"></ToDoEdit>
      <ToDoDelete @task-deleted="deleteTask" :index="index" class="style-bouton-mode-normal"></ToDoDelete>
    </div>
    <div v-else>
      <ToDoDelete @task-deleted="deleteTask" :index="index"></ToDoDelete>
      <ToDoConfirmEdit @edit-confirmed="confirmEdit" :index="index"></ToDoConfirmEdit>
      <ToDoCancelEdit @edit-canceled="toggleTaskIsEditing"></ToDoCancelEdit>
    </div>
  </div>
</template>

<script>
import ToDoChecked from './Task/ToDoIsChecked.vue';
import ToDoName from './Task/ToDoName.vue';
import ToDoDelete from './Task/ToDoDelete.vue';
import ToDoEdit from './Task/ToDoEdit.vue';
import ToDoConfirmEdit from './Task/ToDoConfirmEdit.vue';
import ToDoCancelEdit from './Task/ToDoCancelEdit.vue';

export default {
  props: ['task', 'index'],

 components: {
  ToDoChecked,
  ToDoName,
  ToDoDelete,
  ToDoEdit,
  ToDoConfirmEdit,
  ToDoCancelEdit
 },

 methods: {
  toggleTaskIsChecked() {
    const updatedTask = {...this.task, isChecked: !this.task.isChecked };
    this.$emit('task-updated', this.index, updatedTask);
  },

  toggleTaskIsEditing() {
    const updatedTask = {...this.task, newName: this.task.name, isEditing: !this.task.isEditing };
    this.$emit('task-updated', this.index, updatedTask);
  },

  deleteTask() {
    this.$emit('task-deleted', this.index);
  },

  confirmEdit() {
    const updatedTask = {...this.task, name: this.task.newName, isEditing: !this.task.isEditing }
    this.$emit('task-updated', this.index, updatedTask);
  },
  
  changeName(newName) {
    const updatedTask = {...this.task, newName: newName}
    this.$emit('task-updated', this.index, updatedTask);
  },
 }
}
</script>

<style>
.alignement {
  display: flex;
}

.style-bouton-mode-normal {
  display: none;
  position: relative;
}

.alignement:hover .style-bouton-mode-normal {
  display: inline-block;
}
</style>