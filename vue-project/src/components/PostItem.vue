<template>
  <div class="post">
    <div class="post-content">
      <div class="name"><strong>{{ post.name }} </strong></div>

      <div><strong>Почта: </strong>{{ post.email }}</div>
      <hr/>
      <div><strong>Описание: </strong>{{ post.body }}</div>
    </div>
    <but class="delete-btn" @click="removeComment">Удалить</but>
  </div>
</template>

<script setup>

import but from './but.vue'
const emit = defineEmits(['remove']);

const props = defineProps({
  post: {
    type: Object,
    required: true
  }
});

const removeComment = () => {
  emit('remove', props.post);
};
</script>

<style scoped>
.post {
  padding: 15px;
  border: 2px solid cadetblue;
  margin-top: 15px;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;

}

strong {
  font-weight: bold;
}
.name {
  color: teal;
  font-size: 14pt;
  margin-bottom: 10px;

}
</style>