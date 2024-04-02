<template>
  <select v-model="selected" @change="changeSelect">
    <option disabled value="">Veuillez en sélectionner un</option>
    <option value="name-asc">Par Ordre de l'alphabet</option>
    <option value="name-desc">Par Ordre inverse de l'alphabet</option>
    <option value="date-desc">Du plus récent au plus vieux</option>
    <option value="date-asc">Du plus vieux au plus récent</option>
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
      console.log(this.selected)
      this.$emit('select-changed', this.selected);
    }
  }
}
</script>
