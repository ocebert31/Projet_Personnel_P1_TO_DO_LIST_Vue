<template>
    <label :for="'checkbox-' + index" :class="{'text-decoration-line-through': task.isChecked }" v-if="!task.isEditing">{{ task.name }}</label>
    <input :for="'checkbox-' + index" v-else type="text" @input="event => changeName(event.target.value)" :value="this.task.newName"/>
</template>

<script>
export default {
  props: ['task', 'index'],

  methods: {
    changeName(newName) {
      if (newName.trim() !== '') {
        this.$emit('name-changed', newName);
      }
    }
  }
}
</script>