<template>
  <form @submit.prevent="addPost">
    <input placeholder="Name" v-model="post.name" />
    <input placeholder="Email" v-model="post.email" />
    <input placeholder="Body" v-model="post.body" />
    <button type="submit">Add</button>
  </form>
</template>

<script setup>
import { ref } from 'vue';

const emit = defineEmits(['create']);

const post = ref({
  name: '',
  email: '',
  body: ''
});

const addPost = () => {
  post.value.id = Date.now();
  emit('create', { ...post.value });
  post.value.name = '';
  post.value.email = '';
  post.value.body = '';
};
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
}
input {
  width: 100%;
  box-sizing: border-box;
  margin-bottom: 15px;
  padding: 10px 15px;
  border: 1px solid teal;
}
</style>