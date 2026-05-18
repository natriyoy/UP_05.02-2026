<template>
  <div v-for="post in posts" :key="post.id">
    <post-item
        :post="post"
        @remove="$emit('remove', post)"
    ></post-item>
  </div>
</template>

<script setup>
import PostItem from "@/components/PostItem.vue";

defineProps({
  posts: {
    type: Array,
    required: true
  }
});

// объявляем событие remove, чтобы прокинуть его в родительский компонент
defineEmits(['remove']);
</script>