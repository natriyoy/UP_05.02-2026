<template>
  <div class="bov">Новый комментарий</div>
  <form @submit.prevent="addPost">
    <input placeholder="Название" v-model="post.name" />
    <input placeholder="Почта" v-model="post.email" />
    <textarea placeholder="Описание" v-model="post.body" />
    <but type="submit">Добавить</but>
  </form>
</template>

<script setup>
import { ref } from 'vue';
import but from './but.vue'

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
textarea {
  width: 100%;
  box-sizing: border-box;
  margin-bottom: 15px;
  padding: 10px 15px;
  border: 1px solid teal;
  height: 100px;
}
.bov {
  padding-bottom: 15px;
  color: teal;
  font-weight: bold;
}
</style>