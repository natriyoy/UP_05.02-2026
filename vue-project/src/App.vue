// разметка
<template>
  <div class="app">
    <h2 style="margin-bottom: 15px">Задание 1. Компонентный подход во Vue</h2>
    <div class="bitst"><but @click="showDialog">Новый комментарий</but></div>
    <my-dialog v-model:show="dialogVisible">
      <post-form @create="addPost"></post-form>
    </my-dialog>
    <div class="sel">
      <my-select v-model="selectedSort" :options="sortOpions"></my-select>
      <my-select v-model="selectedOrder" :options="orderOptions"></my-select>
    </div>




      <my-input class="sort"
          v-model="searchName"
          placeholder="Поиск по имени..."
      ></my-input>

      <my-input class="sort"
          v-model="searchBody"
          placeholder="Поиск по тексту..."
      ></my-input>

    <h2>Список комментариев</h2>
    <h2 class="bl" v-if="sortedPost.length<1">Список пуст</h2>
    <div class="posts-grid">
      <post-list :posts="sortedPost" @remove="deletePost"></post-list>
    </div>

  </div>

</template>

// код
<script setup>
import but from './components/but.vue';

import PostList from './components/PostList.vue';
import PostForm from './components/PostForm.vue';

import {ref, onMounted, computed} from 'vue';
import MySelect from "@/components/MySelect.vue";
import MyInput from './components/MyInput.vue';
import MyDialog from "@/components/MyDialog.vue";



const posts = ref([]);

const selectedSort = ref("");
const selectedOrder = ref("asc");

const searchName = ref("");
const searchBody = ref("");

const dialogVisible = ref(false);

const sortOpions = ref([
  {value: 'name', name: 'По имени'},
    {value: 'email', name: 'По почте'},
    {value: 'body', name: 'По описанию'}
]);
const orderOptions = ref([
  { value: 'asc', name: 'По возрастанию' },
  { value: 'desc', name: 'По убыванию' }
]);
const showDialog = () => {
  dialogVisible.value = true;
};
const sortedPost = computed(() => {
  let result = [...posts.value];

  // Фильтрация по имени
  if (searchName.value.trim()) {
    result = result.filter(post =>
        post.name.toLowerCase().includes(searchName.value.toLowerCase().trim())
    );
  }

  // Фильтрация по тексту
  if (searchBody.value.trim()) {
    result = result.filter(post =>
        post.body.toLowerCase().includes(searchBody.value.toLowerCase().trim())
    );
  }

  // Сортировка
  if (selectedSort.value) {
    result.sort((a, b) => {
      const aVal = a[selectedSort.value];
      const bVal = b[selectedSort.value];

      if (selectedOrder.value === 'asc') {
        return aVal.localeCompare(bVal);
      } else {
        return bVal.localeCompare(aVal);
      }
    });
  }

  return result;
});
onMounted(async () => {
  const response = await fetch('comments.json');
  posts.value = await response.json();
});

// функция добавления поста
const addPost = (post) => {
  posts.value.unshift(post);
  dialogVisible.value = false;
};

// функция удаления поста
const deletePost = (post) => {
  posts.value = posts.value.filter(p => p.id !== post.id);
};
</script>


<style scoped>
.app {
  min-width: 1200px;
  padding: 20px;


}
.posts-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 20px;
}
h2 {
  text-align: center;
  padding: 0 20px 0px 20px;
  font-weight: bold;

}
.sort {
  margin-bottom: 15px;
}
.sel {
  display: flex;
  gap: 10px;
  margin-top: 15px;
}

.bl {
  border: 3px dashed teal;
  margin-top: 15px;
  padding: 20px;
}
.bitst {
  border: 3px dashed teal;
  padding: 2px;
}
</style>