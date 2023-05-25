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
    addStar(id) {
      this.$emit("add-Star", id);
    },
    delStar(id) {
      this.$emit("del-Star", id);
    },
  },
};
</script>

<template>
  <div class="busca-post">
    <input
      id="inputBusca"
      placeholder="procure pelo título do post"
      v-model="search"
      @keyup="filteredPosts"
    />
    <span class="material-symbols-sharp fa-search"> search </span>
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
      <div class="divTituloData">
        <h3>{{ post.title }}</h3>
        &nbsp;
        <h3>
          {{ post.datetime }}
        </h3>
      </div>
      <textarea cols="20" rows="10" class="textareaHome"
        >{{ post.content.substring(0, 565) }}...</textarea
      >

      <img :src="post.image" class="imagePost" />
      <div class="stars">
        <span
          class="material-symbols-sharp iconStar"
          @click="delStar(getPostId(post.title))"
        >
          remove
        </span>
        <span class="material-symbols-sharp iconStar"> grade </span>
        <p class="starcount">{{ post.star }}</p>
        <span
          class="material-symbols-sharp iconStar"
          @click="addStar(getPostId(post.title))"
        >
          add
        </span>
      </div>
    </div>

    <div class="modal" v-show="showModal">
      <div class="divModalHelpCabecalho">
        <div class="flexCenter">Deletar Post?</div>
        <div class="textoModalHelp">
          <p>
            Você tem certeza que quer delevar o post? '{{
              selectedPost?.title
            }}'
          </p>
        </div>
        <div class="modal-actions">
          <button class="bg-error" @click="setupModal">
            <span class="material-symbols-sharp iconeButtons"> close </span
            >Cancelar
          </button>

          <button class="bg-success" @click="deletePost">
            <span class="material-symbols-sharp iconeButtons"> check </span>
            Confirmar
          </button>
        </div>
      </div>
    </div>
    <div v-if="filteredPosts == ''" class="nenhumPost">
      Que pena, nenhum post ainda =(
    </div>
  </div>
</template>
