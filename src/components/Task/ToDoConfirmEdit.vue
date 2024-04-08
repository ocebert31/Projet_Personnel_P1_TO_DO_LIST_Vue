<template>
    <button @click="confirmEdit" class="bg-white border border-0 text-success">
      <font-awesome-icon icon="fa-check" />
    </button>
</template>

<script>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
    
export default {
  components: {
    FontAwesomeIcon,
  },

  methods: {
    confirmEdit() {
        this.$emit('edit-confirmed'); 
    }
  }
}
</script>