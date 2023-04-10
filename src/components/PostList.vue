<template>
  <div v-show="posts.length > 0">
    <h2>Список пользователей</h2>
    <post-item :post="post" v-for="post in posts" :key="post.id" @remove="$emit('remove', post)" />
  </div>
  <div v-show = "posts.length === 0">
    <h2>Нет постов</h2>
  </div>
</template>

<script>
import PostItem from "./PostItem.vue";
export default {
  components: { PostItem },
  props: {
    posts: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped></style>
