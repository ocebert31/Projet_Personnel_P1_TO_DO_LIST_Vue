<template>
  <div>
    <button @click="openConfirmationDialog" class="btn btn-outline btn-sm">
      <font-awesome-icon icon="fa-rotate-right" />
      Tout supprimer
    </button>
    <div v-if="showConfirmationDialog" class="modal fade show" tabindex="-1" role="dialog">
      <div class="modal-dialog" role="document">
        <div class="modal-content">
          <div class="modal-header bg-light">
            <h5 class="modal-title">Confirmation</h5>
            <button type="button" class="close" @click="closeConfirmationDialog">
              <span>&times;</span>
            </button>
          </div>
          <div class="modal-body">
            <p>Voulez-vous vraiment tout supprimer ?</p>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-success" @click="confirmClearTasks">Oui</button>
            <button type="button" class="btn btn-danger" @click="closeConfirmationDialog">Non</button>
          </div>
        </div>
      </div>
    </div>
    <div v-if="showConfirmationDialog" class="modal-backdrop fade show"></div>
  </div>
</template>

<script>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'

export default {
  components: {
    FontAwesomeIcon
  },

  data() {
    return {
      showConfirmationDialog: false
    };
  },

  methods: {
    openConfirmationDialog() {
      console.log('pouet');
      this.showConfirmationDialog = true;
    },

    closeConfirmationDialog() {
      this.showConfirmationDialog = false;
    },

    confirmClearTasks() {
      this.$emit('tasks-cleared', this.index);
      this.closeConfirmationDialog();
    }
  }
}
</script>

<style scoped>
.modal.fade.show {
  display: block !important;
}
</style>
