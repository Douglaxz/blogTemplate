<script>
import { handleError } from "vue";
import { RouterLink, RouterView } from "vue-router";

import "@/assets/base.css";

export default {
  data() {
    return {
      /*variável para mostrar o modal de ajuda*/
      showHelp: false,
      posts: [
        {
          title: "Javascript",
          content:
            "JavaScript é uma linguagem de programação de alto nível, interpretada e orientada a objetos. Ela é amplamente usada no desenvolvimento web para criar interações dinâmicas e funcionais em páginas da web. JavaScript é uma linguagem versátil que permite a criação de aplicativos web, desenvolvimento de jogos, criação de aplicativos móveis e muito mais.Principais características do JavaScript:Linguagem baseada em scripts: JavaScript é executado diretamente no navegador, não requerendo um processo de compilação separado. Isso torna o desenvolvimento rápido e ágil.Integração com HTML e CSS: JavaScript pode interagir com elementos HTML e estilos CSS, permitindo manipulação e modificação dinâmica do conteúdo e do layout de uma página da web.Orientação a objetos: JavaScript suporta programação orientada a objetos, permitindo a criação de objetos, classes, herança e polimorfismo. Funcionalidades assíncronas: JavaScript possui recursos que permitem executar tarefas de forma assíncrona, como requisições HTTP, manipulação de eventos e animações, melhorando a responsividade e a experiência do usuário.Bibliotecas e frameworks populares: Existem inúmeras bibliotecas e frameworks construídos em JavaScript, como React, Angular e Vue.js, que facilitam o desenvolvimento de aplicativos web complexos. Suporte à programação do lado do cliente e do lado do servidor: JavaScript pode ser executado tanto no lado do cliente, no navegador do usuário, como no lado do servidor, usando o ambiente Node.js. Compatibilidade com múltiplos navegadores: JavaScript é suportado por todos os principais navegadores web, garantindo que os aplicativos sejam executados em diferentes plataformas e dispositivos. JavaScript desempenha um papel fundamental no desenvolvimento web moderno, permitindo a criação de páginas interativas, aplicativos web avançados e experiências de usuário envolventes. Sua popularidade e ampla adoção tornaram-no uma habilidade essencial para os desenvolvedores web.",
          image:
            "https://logowik.com/content/uploads/images/3799-javascript.jpg",
          datetime: new Date().toLocaleString("pt-BR"),
          star: 0,
        },
        {
          title: "Vue.js",
          content:
            "Vue.js é um framework JavaScript progressivo para a construção de interfaces de usuário. Ele é amplamente utilizado no desenvolvimento web para criar aplicativos de página única (SPA) e interfaces interativas. Vue.js é conhecido por sua abordagem simples e fácil de aprender, combinando recursos de outros frameworks e bibliotecas populares. Principais características do Vue.js: Componentização: Vue.js baseia-se no conceito de componentes reutilizáveis. Os componentes encapsulam código HTML, CSS e JavaScript relacionados, permitindo a criação de interfaces modulares e de fácil manutenção. Binding bidirecional: Vue.js oferece binding de dados bidirecional entre o modelo (state) e a visualização (DOM). Isso significa que qualquer alteração no estado é refletida automaticamente na interface do usuário e vice-versa, proporcionando uma sincronização fácil e eficiente. Diretivas: O Vue.js possui diretivas que permitem estender a funcionalidade do HTML, adicionando comportamentos dinâmicos aos elementos. Diretivas populares incluem v-if, v-for e v-on, que permitem controlar renderização condicional, iteração de listas e manipulação de eventos. Reatividade: O Vue.js usa um sistema de reatividade para rastrear dependências e atualizar automaticamente a interface do usuário sempre que os dados mudam. Isso elimina a necessidade de manipulação manual do DOM, tornando o desenvolvimento mais eficiente. Ecossistema extensível: Vue.js possui uma ampla gama de bibliotecas e plugins disponíveis, permitindo a integração com ferramentas populares de desenvolvimento, como Vue Router para roteamento, Vuex para gerenciamento de estado e Vuetify para componentes de interface de usuário pré-construídos. Suporte a Single-File Components (SFC): Vue.js permite a criação de componentes em um único arquivo .vue, que encapsula código HTML, CSS e JavaScript em uma única unidade coesa. Isso facilita a organização e manutenção do código. Curva de aprendizado suave: Vue.js é conhecido por sua curva de aprendizado suave, tornando-o acessível para desenvolvedores iniciantes e experientes. Sua sintaxe intuitiva e documentação abrangente ajudam os desenvolvedores a se tornarem produtivos rapidamente. Vue.js é uma escolha popular para o desenvolvimento de aplicativos web modernos devido à sua flexibilidade, desempenho e simplicidade. Ele combina os melhores recursos de outros frameworks, fornecendo uma experiência de desenvolvimento agradável e eficiente. Com uma comunidade ativa e crescente, Vue.js continua a evoluir e se tornar uma ferramenta de destaque no desenvolvimento web.",
          image:
            "https://upload.wikimedia.org/wikipedia/commons/thumb/9/95/Vue.js_Logo_2.svg/555px-Vue.js_Logo_2.svg.png",
          datetime: new Date().toLocaleString("pt-BR"),
          star: 0,
        },
      ],
    };
  },
  /*função para carregar o conteúdo dos posts da localstorage*/
  created() {
    const postsString = localStorage.getItem("posts");
    if (postsString) {
      this.posts = JSON.parse(postsString);
    }
  },
  methods: {
    addPost(newPost) {
      this.posts.push(newPost);
      this.savePostsToLocalStorage();
    },
    updatePost(updatedPost, id) {
      this.posts[id] = updatedPost;
      this.savePostsToLocalStorage();
    },
    removePost(id) {
      this.posts.splice(id, 1);
      this.savePostsToLocalStorage();
    },
    addStar(id) {
      this.posts[id].star++;
      this.savePostsToLocalStorage();
    },
    delStar(id) {
      if (this.posts[id].star > 0) {
        this.posts[id].star--;
        this.savePostsToLocalStorage();
      }
    },
    savePostsToLocalStorage() {
      const postsString = JSON.stringify(this.posts);
      localStorage.setItem("posts", postsString);
    },
    setupHelp() {
      this.showHelp = !this.showHelp;
    },
  },
};
</script>

<template>
  <header>
    <div class="flexCenter">
      <RouterLink to="/"
        ><span class="material-symbols-sharp icone"> home </span></RouterLink
      >
      <RouterLink to="/create">
        <span class="material-symbols-sharp icone">
          add_circle
        </span></RouterLink
      >
      <span class="material-symbols-sharp icone" @click="setupHelp()">
        question_mark
      </span>
    </div>
  </header>
  <main>
    <RouterView
      :posts="posts"
      @create-post="addPost"
      @edit-post="updatePost"
      @delete-post="removePost"
      @add-star="addStar"
      @del-star="delStar"
    />
    <div class="modal" v-show="showHelp">
      <div class="divModalHelpCabecalho">
        <div class="flexCenter">Ajuda</div>
        <div class="textoModalHelp">
          <p>
            Geral:<br />
            <span class="material-symbols-sharp"> home </span> - Acessar a
            pagina inicial<br />
            <span class="material-symbols-sharp"> add_circle </span> - Criar um
            novo post<br />
            &nbsp;<br />
            No post:<br />
            <span class="material-symbols-sharp"> edit </span> - Editar post<br />
            <span class="material-symbols-sharp"> visibility </span> -
            Visualizar post<br />
            <span class="material-symbols-sharp"> delete </span> - Apagar post
          </p>
        </div>
        <div class="footerModalHelp">
          <span class="material-symbols-sharp icone" @click="setupHelp">
            close
          </span>
        </div>
      </div>
    </div>
  </main>
  <footer>
    <span class="material-symbols-sharp"> chat </span> Um belo blog
    <span class="material-symbols-sharp"> chat </span>
  </footer>
</template>

<style scoped></style>
