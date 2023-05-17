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
  <RouterLink to="/create">Novo Post</RouterLink>
  <RouterLink to="/">Home</RouterLink>
  <RouterView :posts="posts" @create-post="addPost" />
</template>

<style scoped>
/*form {
  display: flex;
  flex-direction: column;
  width: 25vw;
}

form > * {
  margin: 1rem;
}

#lista-post {
  background-color: purple;
  margin-left: 25vw;
  width: 50vw;
  padding: 15px;
}

.post {
  background-color: white;
  width: 95%;
  margin: 15px;
  border: 2px solid black;
  border-radius: 15px;
  font-family: Arial, Helvetica, sans-serif;
}
*/
</style>
