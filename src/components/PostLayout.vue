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
      },
      isEditing: Boolean(this.post),
    };
  },
  methods: {
    handleClickCreatePost(event) {
      alert(id);
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
  },
};
</script>
<template>
  <form>
    <label>Visualizar Post</label>
  </form>
  <div id="lista-post">
    <div class="post">
      <h3>
        {{ post.title }}
        <RouterLink :to="`/`">
          <span class="material-symbols-sharp icone"> reply </span>
        </RouterLink>
      </h3>
      <h4>{{ post.datetime }}</h4>
      <p>{{ post.content }}</p>
    </div>
  </div>
</template>
