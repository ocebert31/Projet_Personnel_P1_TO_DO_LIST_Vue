<template>
  <select v-model="selected" @change="changeSelect" class="form-select border border-dark">
    <option value="date-asc"></option>
    <option value="name-asc" class="bg-secondary text-white">Par Ordre de l'alphabet</option>
    <option value="name-desc" class="bg-secondary text-white">Par Ordre inverse de l'alphabet</option>
    <option value="date-desc" class="bg-secondary text-white">Du plus récent au plus vieux</option>
    <option value="date-asc" class="bg-secondary text-white">Du plus vieux au plus récent</option>
    <option value="precedence-desc" class="bg-secondary text-white">Priorité croissante</option>
    <option value="precedence-asc" class="bg-secondary text-white">Priorité décroissante</option>
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
