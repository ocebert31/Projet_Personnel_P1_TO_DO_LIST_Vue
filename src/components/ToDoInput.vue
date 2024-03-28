<template>
    Ajout: <input type="text" v-model="task"/>
    <button @click="addTaskToList">Valider</button>
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
