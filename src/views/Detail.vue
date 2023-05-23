<script>
import { RouterLink } from "vue-router";
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
    PostLayout,
  },
};
</script>

<template>
  <PostLayout :post="post"></PostLayout>
</template>
