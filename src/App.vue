<script>
import { handleError } from "vue";
import { RouterLink, RouterView } from "vue-router";

export default {
  data() {
    return {
      posts: [
        {
          title: "Meu primeiro post",
          datetime: Date.now(),
          content: "postar aqui é bem legal",
        },
        {
          title: "Meu segundo post",
          datetime: Date.now(),
          content: "postar aqui é bem mais legal",
        },
      ],
      FormData: {
        title: "",
        content: "",
      },
    };
  },
  methods: {
    handleClick(event) {
      console.log(this.FormData);

      const now = new Date();


      const datadaPostagem = `${now.getDate()}/${now.getMonth() + 1;}/${now.getFullYear()}`;

      this.posts.push({
        title: this.FormData.title,
        datetime: datadaPostagem,
        content: this.FormData.content,
      });
      this.FormData = {
        title: "",
        content: "",
      };
    },
    handleInputChange(event) {
      const { name, value } = event.target;
      this.FormData[name] = value;
    },
  },
};
</script>

<template>
  <div id="lista-post">
    <div class="post" v-for="post in posts" :key="post.title">
      <h3>{{ post.title }}</h3>
      <h4>{{ post.datetime }}</h4>
      <p>{{ post.content }}</p>
    </div>
  </div>
  <form>
    <label> Título </label>
    <input
      type="text"
      name="title"
      placeholder="digite seu título"
      @keyup="handleInputChange"
      :value="FormData.title"
    />
    <label> Texto do post </label>
    <textarea
      name="content"
      placeholder="digite seu post aqui"
      id=""
      cols="30"
      rows="10"
      @keyup="handleInputChange"
      :value="FormData.content"
    >
    </textarea>
    <button type="button" @click="handleClick">Enviar</button>
  </form>

  <RouterView />
</template>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  width: 25vw;
}

form > * {
  margin: 1rem;
}
</style>
