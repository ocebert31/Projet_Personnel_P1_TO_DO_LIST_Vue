<template>
  <div>
    <button @click="openConfirmationDialog" class="btn btn-outline btn-sm">
      <font-awesome-icon icon="fa-rotate-right" />
      Tout supprimer
    </button>
    <div v-if="showConfirmationDialog" class="clear-modal">
      <div class="clear-modal-content">
        <span class="close" @click="closeConfirmationDialog">&times;</span>
        <h2>Confirmation</h2>
        <p>Voulez-vous vraiment tout supprimer ?</p>
        <button @click="confirmClearTasks">Oui</button>
        <button @click="closeConfirmationDialog">Non</button>
      </div>
    </div>
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

<style>
.clear-modal {
  display: block;
  position: fixed;
  z-index: 9999;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
}

.clear-modal-content {
  background-color: #fff;
  margin: 10% auto;
  padding: 20px;
  border: 1px solid #888;
  width: 80%;
}

.close {
  color: #aaa;
  float: right;
  font-size: 28px;
  font-weight: bold;
  cursor: pointer;
}

.close:hover,
.close:focus {
  color: black;
  text-decoration: none;
  cursor: pointer;
}
</style>
