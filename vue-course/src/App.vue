<template>
  <div class="app">
    <h1>Posts page</h1>
    <my-button @click="showDialog" style="margin: 15px">Create post</my-button>
    <my-dialog v-model:show="dialogVisible">
      <post-form @create="createPost" />
    </my-dialog>

    <post-list :posts="posts" @remove="removePost" v-if="!arePostsLoading" />
  </div>
  <h1 v-if="arePostsLoading">Loading...</h1>
</template>

<script>
import PostFormVue from "@/components/PostForm.vue";
import PostListVue from "@/components/PostList.vue";
import axios from "axios";

export default {
  components: {
    PostForm: PostFormVue,
    PostList: PostListVue,
  },
  data() {
    return {
      posts: [],
      dialogVisible: {
        type: Boolean,
        default: false,
      },
      modificatorValue: "",
      arePostsLoading: true,
    };
  },
  methods: {
    createPost(post) {
      this.posts.push(post);
      this.title = "";
      this.body = "";
      this.dialogVisible = false;
    },
    removePost(post) {
      this.posts = this.posts.filter((item) => item.id !== post.id);
    },
    showDialog() {
      this.dialogVisible = true;
    },
    async fetchPosts() {
      try {
        setTimeout(async () => {
          const response = await axios.get(
            "https://jsonplaceholder.typicode.com/posts?_limit=10"
          );
          this.posts = response.data;
          this.arePostsLoading = false;
        }, 1000);
      } catch (e) {
        alert("Error");
      }
    },
  },
  mounted() {
    this.fetchPosts();
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.app {
  padding: 20px;
}
</style>
