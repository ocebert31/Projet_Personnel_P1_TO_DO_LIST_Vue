<template>
    <button @click="deleteTask" class="bg-white border border-0 text-danger">
      <font-awesome-icon icon="fa-trash" />
    </button>
</template>
    
<script>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
    
export default {
  components: {
    FontAwesomeIcon,
  },

  props: ['index'],

  methods: {
    deleteTask() {
      this.$emit('task-deleted', this.index); 
    }
  }
}
</script>
  