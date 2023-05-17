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
      <RouterLink to="/create">Novo Post</RouterLink> |
      <RouterLink to="/">Home</RouterLink>
    </nav>
  </header>

  <RouterView :posts="posts" @create-post="addPost" />
</template>

<style scoped></style>
