<template>
    <select v-model="selected" @change="handleSelection">
      <option disabled value="">Veuillez en sélectionner un</option>
      <option>Ordre initial</option>
      <option>Par Ordre de l'alphabet</option>
      <option>Par Ordre inverse de l'alphabet</option>
      <option>Du plus récent au plus vieux</option>
      <option>Du plus vieux au plus récent</option>
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
      handleSelection() {
        if (this.selected === "Par Ordre de l'alphabet") {
          this.filterOrderAlphabetiqueEmit();
        } else if (this.selected === "Par Ordre inverse de l'alphabet") {
          this.filterDesorderAlphabetiqueEmit();
        } else if (this.selected === "Du plus récent au plus vieux") {
        this.filterMostRecentToOldest();
        }
      },
      filterOrderAlphabetiqueEmit() {
        this.$emit('alphabétique-order-filtered');
      },
      filterDesorderAlphabetiqueEmit() {
        this.$emit('alphabétique-desorder-filtered');
      },
      filterMostRecentToOldest() {
        this.$emit('filter-most-recent-to-oldest');
      },
    },
  };
  </script>
  