<script>
import { RouterLink } from "vue-router";
import PostForm from "@/components/PostForm.vue";
export default {
  props: {
    posts: Array,
  },
  data() {
    const id = this.$route.params.id;

    return {
      id: id,
      post: this.posts[id],
    };
  },
  components: {
    PostForm,
  },
};
</script>

<template>
  <PostForm :post="post" :id="id"></PostForm>
</template>
