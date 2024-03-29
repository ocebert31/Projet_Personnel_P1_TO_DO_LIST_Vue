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

  props: ['index'],

  methods: {
    confirmEdit() {
        this.$emit('edit-confirmed', this.index); 
    }
  }
}
</script>