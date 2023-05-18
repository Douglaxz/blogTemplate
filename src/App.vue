<script>
import { handleError } from "vue";
import { RouterLink, RouterView } from "vue-router";

import "@/assets/base.css";

export default {
  data() {
    return {
      posts: [],
    };
  },
  methods: {
    addPost(newPost) {
      this.posts.push(newPost);
    },
  },
};
</script>

<template>
  <header>
    <nav>
      |
      <RouterLink to="/">Home</RouterLink> |
      <RouterLink to="/create">New</RouterLink> |
    </nav>
  </header>

  <RouterView :posts="posts" @create-post="addPost" />
  <footer>Um belo blog</footer>
</template>

<style scoped></style>
