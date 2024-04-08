<template>
  <select v-model="selected" @change="changeSelect" class="form-select border border-dark">
    <option value="date"></option>
    <option value="name" class="bg-secondary text-white">Par Ordre Alphabétique</option>
    <option value="date" class="bg-secondary text-white">Par Ordre Chronologique</option>
    <option value="precedence" class="bg-secondary text-white">Par Ordre de Priorité</option>
  </select>
</template>
  
<script>
export default {
  data() {
    return {
      selected: "",
    };
  },

  methods: {
    changeSelect() {
      this.$emit('select-changed', this.selected);
    }
  }
}
</script>

<style>
 .bg-secondary {
  font-size: 14px;
 }
</style>
