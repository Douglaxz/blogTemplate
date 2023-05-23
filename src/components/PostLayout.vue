<script>
export default {
  props: {
    post: Object,
  },
  data() {
    const id = this.$route.params.id;
    return {
      FormData: {
        title: this.post?.title || "",
        content: this.post?.content || "",
      },
      isEditing: Boolean(this.post),
      id: id,
    };
  },
  methods: {
    handleClickCreatePost(event) {
      if (!this.FormData.title || !this.FormData.content) {
        alert("Por favo preencha todos os campos");
        return;
      }
      const datadaPostagem = new Date().toLocaleString("pt-BR");

      const postData = {
        title: this.FormData.title,
        content: this.FormData.title,
        datetime: datadaPostagem,
      };

      if (isEditing) {
        this.$emit("edit-post", postData, this.id);
      } else {
        this.$emit("create-post", postData);
      }

      this.FormData = {
        title: "",
        content: "",
      };

      this.$router.push("/");
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
  <div id="lista-post">
    <div class="post">
      <div class="flex">
        Visualizar Post
        <RouterLink :to="`/edit/${id}`">
          <span class="material-symbols-sharp icone"> edit </span>
        </RouterLink>
        <RouterLink :to="`/`">
          <span class="material-symbols-sharp icone"> reply </span>
        </RouterLink>
      </div>
      <div class="divTituloData">
        <h3>{{ post.title }}</h3>
        &nbsp;
        <h3>
          {{ post.datetime }}
        </h3>
      </div>
      <textarea cols="20" rows="10" class="textareaHome">{{
        post.content
      }}</textarea>
      <img :src="post.image" class="imagePost" />
      <div class="stars">
        <span class="material-symbols-sharp iconStar" @click="delStar(id)">
          keyboard_double_arrow_left
        </span>
        <span class="material-symbols-sharp iconStar"> grade </span>
        <p class="starcount">{{ post.star }}</p>

        <span class="material-symbols-sharp iconStar" @click="addStar(id)">
          keyboard_double_arrow_right
        </span>
      </div>
    </div>
  </div>
</template>
