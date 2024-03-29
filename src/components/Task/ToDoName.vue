<template>
    <label :for="'checkbox-' + index" :class="{ 'styled': task.isChecked }" v-if="!isEditing">{{ task.name }}</label>
    <input :for="'checkbox-' + index" v-else type="text" @input="event => changeName(event.target.value)" :value="newName"/>
</template>

<script>
export default {
  props: ['task', 'index', 'isEditing', 'newName'],

  methods: {
    changeName(newName) {
      if (newName.trim() !== '') {
        this.$emit('name-changed', newName);
      }
    }
  }
}
</script>

<style scoped>
  .styled {
    text-decoration: line-through;
  }
</style>