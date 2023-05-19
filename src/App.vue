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
          datetime: new Date().toLocaleString("pt-BR"),
          content: "meu lindo post",
        },
      ],
    };
  },
  methods: {
    addPost(newPost) {
      alert(newPost.datetime);
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
      |&nbsp;
      <span class="material-symbols-sharp"> home </span>
      <RouterLink to="/">Home</RouterLink>
      &nbsp; |&nbsp;
      <span class="material-symbols-sharp"> add_circle </span>
      <RouterLink to="/create"> New</RouterLink>
      &nbsp; |
    </nav>
  </header>
  <main>
    
    <RouterView :posts="posts" @create-post="addPost" @edit-post="updatePost" />
  </main>
  <footer>
    <span class="material-symbols-sharp"> chat </span> Um belo blog
    <span class="material-symbols-sharp"> chat </span>
  </footer>
</template>

<style scoped></style>
