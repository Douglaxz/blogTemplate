<script>
import { RouterLink } from "vue-router";

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
  methods: {
    getPostId(title) {
      for (const index in this.posts) {
        const post = this.posts[index];
        if (post.title === title) return index;
      }
    },
  },
};
</script>

<template>
  <div id="busca-post">
    <div id="pesquisa-post">
      <input
        id="inputBusca"
        placeholder="procure pelo título do post"
        v-model="search"
        @keyup="filteredPosts"
      />
    </div>
  </div>
  <div id="lista-post">
    <div class="post" v-for="(post, index) in filteredPosts" :key="post.title">
      <h3>
        {{ post.title }}
        <RouterLink :to="`/edit/${getPostId(post.title)}`">
          <span class="material-symbols-sharp icone"> edit </span>
        </RouterLink>
        <span class="material-symbols-sharp"> visibility </span>
      </h3>
      <h4>{{ post.datetime }}</h4>
      <p>{{ post.content }}</p>
    </div>
    <div v-if="filteredPosts == ''" class="nenhumPost">
      Que pena, nenhum post ainda =(
    </div>
  </div>
</template>
