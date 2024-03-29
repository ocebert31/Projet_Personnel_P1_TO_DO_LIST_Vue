<template>
  <div class="alignement">
    <ToDoChecked :task="task" :index="index" @toggle-task-checked="toggleTaskIsChecked"></ToDoChecked>
    <ToDoName :task="task" :index="index" :isEditing="isEditing"></ToDoName>
  <div v-if="!isEditing" style="display: flex;">
    <ToDoEdit @edit-mode-toggled="toggleEditMode" class="style-bouton-mode-normal"></ToDoEdit>
    <ToDoDelete @task-deleted="deleteTask" :index="index" class="style-bouton-mode-normal"></ToDoDelete>
  </div>
  <div v-else>
    <ToDoDelete @task-deleted="deleteTask" :index="index"></ToDoDelete>
    <ToDoConfirmEdit @edit-confirmed="confirmEdit" :index="index" :isValidate="isValidate"></ToDoConfirmEdit>
    <ToDoCancelEdit @edit-canceled="toggleEditMode"></ToDoCancelEdit>
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

 data() {
    return {
      isEditing: false,
      isValidate:false,
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

  confirmEdit() {
    const editedTask = {name: this.task.name, isValidate: !this.task.isValidate}
    this.$emit()('confirmed-edit', this.index, editedTask)
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