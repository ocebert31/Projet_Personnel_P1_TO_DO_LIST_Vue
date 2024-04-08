<template>
    <button @click="toggleEditMode" class="bg-white border border-0 text-primary">
      <font-awesome-icon icon="fa-pen" />
    </button>
</template>

<script>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
    
export default {
  components: {
    FontAwesomeIcon,
  },

  methods: {
    toggleEditMode() {
      this.$emit('edit-mode-toggled'); 
    }
  }
}
</script>

