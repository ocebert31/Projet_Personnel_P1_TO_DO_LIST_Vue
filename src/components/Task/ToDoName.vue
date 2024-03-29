<template>
    <label :for="'checkbox-' + index" :class="{ 'styled': task.isChecked }" v-if="!isEditing">{{ task.name }}</label>
    <input :for="'checkbox-' + index" v-else :value="task.name" type="text" />
</template>

<script>
export default {
    props: ['task', 'index', 'isEditing'],
}
</script>

<style scoped>
  .styled {
    text-decoration: line-through;
  }
</style>