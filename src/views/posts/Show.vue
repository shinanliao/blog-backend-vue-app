<template>
  <div class="posts-show">
    <h2>{{ post.title }}</h2>
    <img :src="post.image" alt="" />
    <p>{{ post.title }}</p>
    <p>{{ post.body }}</p>
    <router-link :to="`/posts/${post.id}/edit`">Edit</router-link>
    <br />
    <button v-on:click="destroyPost()">Delete Post</button>
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
  methods: {
    destroyPost: function () {
      if (confirm("Are you sure you want to delete this post?")) {
        axios.delete(`/posts/${this.post.id}`).then((response) => {
          console.log(response.data);
          this.$router.push("/posts");
        });
      }
    },
  },
};
</script>
