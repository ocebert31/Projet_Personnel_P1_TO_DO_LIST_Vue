<template>
  <div class="input-group mb-3">
    <input type="text" v-model="task" placeholder="Ajoute une tâche" class="form-control rounded-start-pill" />
    <button @click="addTaskToList" class="btn btn-success">Valider</button>
  </div>
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
