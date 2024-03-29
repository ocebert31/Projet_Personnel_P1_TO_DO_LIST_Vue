<template>
    <button @click="toggleEditMode">
      <font-awesome-icon icon="fa-pen" />
    </button>
</template>

<script>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
    
export default {
    components: {
      FontAwesomeIcon
    },
  
    methods: {
        toggleEditMode() {
          this.$emit('edit-mode-toggled'); 
        }
    }
}
</script>

