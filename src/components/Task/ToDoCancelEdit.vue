<template>
    <button @click="cancelEdit">
      <font-awesome-icon icon="fa-xmark" />
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
    cancelEdit() {
        this.$emit('edit-canceled', this.index); 
    }
  }
}
</script>