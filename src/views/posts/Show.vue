<template>
  <div class="posts-show">
    <h2>{{ post.title }}</h2>
    <img :src="post.image" alt="" />
    <p>{{ post.title }}</p>
    <p>{{ post.body }}</p>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      post: {},
    };
  },
  created: function () {
    axios.get(`/posts/${this.$route.params.id}`).then((response) => {
      console.log("Post object", response.data);
      this.post = response.data;
    });
  },
};
</script>
