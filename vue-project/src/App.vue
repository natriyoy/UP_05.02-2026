// разметка
<template>
  <div class="app">
    <post-form @create="addPost"></post-form>
    <h3>Список комментариев</h3>
    <post-list :posts="posts" @remove="deletePost"></post-list>
  </div>
</template>

// код
<script setup>
import PostList from './components/PostList.vue';
import PostForm from './components/PostForm.vue';

import { ref, onMounted } from 'vue';

const posts = ref([]);

onMounted(async () => {
  const response = await fetch('comments.json');
  posts.value = await response.json();
});

// функция добавления поста
const addPost = (post) => {
  posts.value.unshift(post);
};

// функция удаления поста
const deletePost = (post) => {
  posts.value = posts.value.filter(p => p.id !== post.id);
};
</script>

// оформление
<style scoped>
.app {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}
</style>