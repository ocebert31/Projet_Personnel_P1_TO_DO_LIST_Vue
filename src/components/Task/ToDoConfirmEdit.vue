<template>
    <button @click="confirmEdit">
      <font-awesome-icon icon="fa-check" />
    </button>
</template>

<script>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
    
export default {
  components: {
    FontAwesomeIcon
  },

  methods: {
    confirmEdit() {
        this.$emit('edit-confirmed'); 
    }
  }
}
</script>