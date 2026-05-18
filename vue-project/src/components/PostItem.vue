<template>
  <div class="post">
    <div>
      <div><strong>Имя: </strong>{{ post.name }}</div>
      <div><strong>Почта: </strong>{{ post.email }}</div>
      <div><strong>Описание: </strong>{{ post.body }}</div>
    </div>
    <button @click="removeComment">Delete</button>
  </div>
</template>

<script setup>
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
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>