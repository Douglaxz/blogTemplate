<script>
import { handleError } from "vue";
import { RouterLink, RouterView } from "vue-router";

export default {
  data() {
    return {
      posts: [
        {
          title: "Meu primeiro post",
          datetime: new Date().toLocaleString("pt-BR"),
          content: "postar aqui é bem legal",
        },
        {
          title: "Meu segundo post",
          datetime: new Date().toLocaleString("pt-BR"),
          content: "postar aqui é bem mais legal",
        },
      ],
      FormData: {
        title: "",
        content: "",
      },
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
    handleClick(event) {
      const datadaPostagem = new Date().toLocaleString("pt-BR");

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
    <div id="pesquisa-post">
      <input
        class="inputPesquisa"
        placeholder="procure pelo título do post"
        v-model="search"
        @keyup="filteredPosts"
      />
    </div>
  </div>
  <div id="lista-post">
    <div class="post" v-for="post in filteredPosts" :key="post.title">
      <h3>{{ post.title }}</h3>
      <h4>{{ post.datetime }}</h4>
      <p>{{ post.content }}</p>
    </div>
  </div>
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

#lista-post {
  background-color: purple;
  margin-left: 25vw;
  width: 50vw;
  padding: 15px;
}

.post {
  background-color: white;
  width: 95%;
  margin: 15px;
  border: 2px solid black;
  border-radius: 15px;
  font-family: Arial, Helvetica, sans-serif;
}

form {
  background-color: purple;
  margin-left: 25vw;
  width: 50vw;
  padding: 15px;
  align-content: center;
  text-align: center;
  align-items: center;
}

label {
  color: white;
  background-color: white;
  color: black;
  border-radius: 15px;
  text-align: center;
  font-family: Arial, Helvetica, sans-serif;
  font-weight: bolder;
  line-height: 40px;
  border: 2px solid black;
  width: 95%;
}

input {
  border: 2px solid black;
  line-height: 35px;
  width: 95%;
  border-radius: 15px;
  font-family: Arial, Helvetica, sans-serif;
}

textarea {
  border: 2px solid black;
  width: 95%;
  border-radius: 15px;
  font-family: Arial, Helvetica, sans-serif;
}

button {
  width: 30%;
  align-items: center;
  background-color: white;
  border-radius: 15px;
  line-height: 30px;
}

button:hover {
  background-color: pink;
  font-weight: bolder;
}
#pesquisa-post {
  margin-left: 15px;
}

::-webkit-input-placeholder {
  color: black;
  font-weight: bold;
}
</style>
