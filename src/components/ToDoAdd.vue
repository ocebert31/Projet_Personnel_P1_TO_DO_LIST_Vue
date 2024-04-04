<template>
    <input type="text" v-model="task" placeholder="Ajoute une tâche" class="form-control" style="border-radius: 5px 0px 0px 5px;"/>
    <button @click="addTaskToList" class="btn btn-primary" style="border-radius: 0px 5px 5px 0px;">Valider</button>
</template>

<script>
export default {
  data() {
    return {
      task: '',
    };
  },

  emits: ['task-added'],

  methods: {
    addTaskToList() {
      if (this.task.trim() !== '') {
        this.$emit('task-added', this.task);
        this.task = '';
      }
    },
  },
};
</script>

<style scoped>
</style>
