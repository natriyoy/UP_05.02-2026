<script setup>
defineEmits(['click'])
</script>

<template>
  <button @click="$emit('click')">
    <slot></slot>
  </button>
</template>

<style scoped>
button {
  padding: 10px 20px;
  background-color: teal;
  color: white;
  border: none;
  cursor: pointer;
  width: 100%;
  font-size: 12pt;
}
</style>