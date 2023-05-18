<script>
export default {
  props: {
    post: Object,
  },
  data() {
    return {
      FormData: {
        title: this.post?.title || "",
        content: this.post?.content || "",
      },
    };
  },
  methods: {
    handleClickCreatePost(event) {
      if (!this.FormData.title || !this.FormData.content) {
        alert("Por favo preencha todos os campos");
        return;
      }
      const datadaPostagem = new Date().toLocaleString("pt-BR");
      this.$emit("create-post", {
        title: this.FormData.title,
        datetime: datadaPostagem,
        content: this.FormData.content,
      });

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
    <label>Novo Post</label>
    <input v-model="FormData.title" placeholder="digite seu titulo aqui" />
    <textarea
      v-model="FormData.content"
      placeholder="digite seu post aqui"
      cols="30"
      rows="10"
    ></textarea>
    <button type="button" @click="handleClickCreatePost">Postar</button>
  </form>
</template>
