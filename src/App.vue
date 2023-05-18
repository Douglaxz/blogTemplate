<script>
import { handleError } from "vue";
import { RouterLink, RouterView } from "vue-router";

import "@/assets/base.css";

export default {
  data() {
    return {
      posts: [
        {
          title: "meu primeiro post",
          datetime: "18/05/2023",
          content: "meu lindo post",
        },
      ],
    };
  },
  methods: {
    addPost(newPost) {
      this.posts.push(newPost);
    },
    updatePost(updatePost, id) {
      this.posts[id] = updatePost;
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
  <main>
    <RouterView :posts="posts" @create-post="addPost" @edit-post="updatePost" />
  </main>
  <footer>Um belo blog</footer>
</template>

<style scoped></style>
