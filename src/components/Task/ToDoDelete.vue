<template>
    <button @click="deleteTask">
      <font-awesome-icon icon="fa-trash" />
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
        deleteTask() {
            // Supprimer l'élément de la liste en utilisant son index
            this.$emit('task-deleted', this.index); // Émettre un événement pour signaler la suppression de la tâche
        }
    }
}
</script>
  