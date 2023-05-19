<script>
import { RouterLink } from "vue-router";
import PostForm from "@/components/PostForm.vue";
import PostLayout from "@/components/PostLayout.vue";
export default {
  props: {
    posts: Array,
  },
  data() {
    return {
      post: this.posts[this.$route.params.id],
    };
  },
  components: {
    PostForm,
    PostLayout,
  },
};
</script>

<template>
  <PostLayout :post="post"></PostLayout>
</template>
