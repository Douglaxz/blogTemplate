<script>
export default {
  data() {
    return {
      FormData: {
        title: "",
        content: "",
      },
    };
  },
  methods: {
    handleClick(event) {
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
    handleInputChange(event) {
      const { name, value } = event.target;
      this.FormData[name] = value;
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
    <button type="button" @click="handleClick">Postar</button>
  </form>
</template>
