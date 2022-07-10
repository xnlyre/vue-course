<template>
  <div v-show="posts.length > 0">
    <h3>Posts list</h3>
    <post-item
      :post="post"
      v-for="post in posts"
      :key="post.id"
      @remove="$emit('remove', post)"
    />
  </div>
  <h3 v-show="posts.length == 0" style="color: red">
    There are not posts here!
  </h3>
</template>

<script>
import PostItemVue from "./PostItem.vue";
export default {
  components: {
    PostItem: PostItemVue,
  },
  props: {
    posts: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped></style>
