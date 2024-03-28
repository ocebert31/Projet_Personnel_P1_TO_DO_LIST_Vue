<template>
    <input type="checkbox" :id="'checkbox-' + index" @click="toggleIsChecked" :checked="task.isChecked" />
</template>

<script>
export default {
  props: ['task', 'index'],

  methods: {
    toggleIsChecked() {
        this.$emit('toggle-task-checked', this.index);
    },
  },
}
</script>