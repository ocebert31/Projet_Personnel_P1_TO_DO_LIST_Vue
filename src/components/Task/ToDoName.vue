<template>
    <label :for="'checkbox-' + index" :class="{ 'styled': task.isChecked }">{{ task.name }}</label>
</template>

<script>
export default {
    props: ['task', 'index'],
}
</script>

<style scoped>
  .styled {
    text-decoration: line-through;
  }
</style>