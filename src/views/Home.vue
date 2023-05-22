<script>
import { RouterLink } from "vue-router";

export default {
  props: {
    posts: Array,
  },
  data() {
    return {
      search: "",
      showModal: false,
      selectedPost: null,
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
    setupModal(id) {
      this.showModal = !this.showModal;
      if (id) {
        this.selectedPost = this.posts[id];
        return;
      }
      this.selectedPost = null;
    },
    deletePost() {
      const id = this.getPostId(this.selectedPost.title);
      this.$emit("delete-post", id);
      this.setupModal();
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
      <div class="flex">
        <RouterLink :to="`/edit/${getPostId(post.title)}`">
          <span class="material-symbols-sharp icone"> edit </span>
        </RouterLink>
        <RouterLink :to="`/detail/${getPostId(post.title)}`">
          <span class="material-symbols-sharp icone"> visibility </span>
        </RouterLink>
        <span
          class="material-symbols-sharp icone"
          @click="setupModal(getPostId(post.title))"
        >
          delete
        </span>
      </div>
      <h3>
        {{ post.title }}
      </h3>
      <h4>{{ post.datetime }}</h4>
      <p>{{ post.content }}</p>
    </div>
    <div class="modal" v-show="showModal">
      <div class="modal-content">
        <h3>Deletar Post</h3>
        <p>
          Você tem certeza que quer delevar o post? '{{ selectedPost?.title }}'
        </p>
        <div class="modal-actions">
          <button class="bg-error" @click="setupModal">Cancelar</button>
          <button class="bg-success" @click="deletePost">Confirmar</button>
        </div>
      </div>
    </div>
    <div v-if="filteredPosts == ''" class="nenhumPost">
      Que pena, nenhum post ainda =(
    </div>
  </div>
</template>
