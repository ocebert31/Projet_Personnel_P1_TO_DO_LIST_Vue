<template>
    <div>
      <input type="checkbox" :id="'checkbox-' + index" v-model="isChecked" />
      <label :for="'checkbox-' + index" :class="{ 'styled': isChecked }">{{ task }}</label>
    </div>
</template>
  
<script>
  export default {
    props: ['task', 'index'],
    data() {
      return {
        isChecked: false
      };
    },
  }
</script>

<style scoped>
  .styled {
    text-decoration: line-through;
  }
</style>