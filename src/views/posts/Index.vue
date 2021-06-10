<template>
  <div class="posts-index">
    <div v-for="post in posts" v-bind:key="post.id">
      <h3>Title: {{ post.title }}</h3>
      <img :src="post.image" alt="" />
      <p>Body: {{ post.body }}</p>
      <router-link :to="`/posts/${post.id}`">More Information</router-link>
      <br />
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
