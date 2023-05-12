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
    };
  },
  methods:{
    handleSubmit(event){
      event.
    }
  }
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
  <form action="" @submit="">
    <label> Título </label>
    <input type="text" name="title" placeholder="digite seu títlo" />
    <label> Texto do post </label>
    <textarea name="content" placeholder="Digite seu post"></textarea>
    <button type="submit" name="btn_submit">Enviar</button>
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
