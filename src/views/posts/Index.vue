<template>
  <div class="posts-index">
    <div v-for="post in posts" v-bind:key="post.id">
      <p>Title: {{ post.title }}</p>
      <p>Body: {{ post.body }}</p>
      <router-link :to="`/posts/${post.id}`">
        <img :src="post.image" alt="" />
      </router-link>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      posts: []
    };
  },
  created: function () {
    axios.get("/posts").then((response) => {
      console.log("Posts array", response.data);
      this.posts = response.data;
    });
  },
};
</script>
