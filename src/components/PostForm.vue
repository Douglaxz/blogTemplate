<script>
export default {
  props: {
    post: Object,
    id: String,
  },
  data() {
    return {
      FormData: {
        title: this.post?.title || "",
        content: this.post?.content || "",
        image: this.post?.image || "",
        star: this.post?.star || "0",
      },
      isEditing: Boolean(this.post),
    };
  },
  methods: {
    handleClickCreatePost(event) {
      if (!this.FormData.title || !this.FormData.content) {
        alert("Por favo preencha todos os campos");
        return;
      }

      const postData = {
        title: this.FormData.title,
        content: this.FormData.content,
        datetime: new Date().toLocaleString("pt-BR"),
        image: this.FormData.image,
        star: this.FormData.star,
      };

      if (this.isEditing) {
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
  },
};
</script>
<template>
  <form>
    <div class="flexPostForm">
      {{ isEditing ? "Editando Post" : "Novo Post" }}
      <span class="material-symbols-sharp icone" @click="handleClickCreatePost">
        save
      </span>
      <RouterLink :to="`/`">
        <span class="material-symbols-sharp icone"> reply </span>
      </RouterLink>
    </div>
    <input v-model="FormData.title" placeholder="digite seu titulo aqui" />
    <textarea
      v-model="FormData.content"
      placeholder="digite seu post aqui"
      cols="30"
      rows="10"
    ></textarea>
    <input v-model="FormData.image" placeholder="digite a url da imagem" />
  </form>
</template>
