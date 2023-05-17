<script>
export default {
  props: {
    posts: Array,
  },
  data() {
    return {
      search: "",
    };
  },
  computed: {
    filteredPosts() {
      if (!this.search) return this.posts;

      const listaFinal = [];
      for (const post of this.posts) {
        if (post.title.includes(this.search)) {
          listaFinal.push(post);
        }
      }
      return listaFinal;
    },
  },
};
</script>

<template>
  <div id="lista-post">
    <div id="pesquisa-post">
      <input
        class="inputPesquisa"
        placeholder="procure pelo título do post"
        v-model="search"
        @keyup="filteredPosts"
      />
    </div>
  </div>
  <div id="lista-post">
    <div class="post" v-for="post in filteredPosts" :key="post.title">
      <h3>{{ post.title }}</h3>
      <h4>{{ post.datetime }}</h4>
      <p>{{ post.content }}</p>
    </div>
  </div>
</template>
