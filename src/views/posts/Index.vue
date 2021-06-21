<template>
  <div class="posts-index">
    <input type="text" v-model="searchTerm" list="title" placeholder="Search" />
    <datalist id="title">
      <option v-for="post in posts" v-bind:key="post.id">
        {{ post.title }}
      </option>
    </datalist>
    <br />
    <button v-on:click="setSortAttribute('title')">Sort by Oldest</button>
    <div v-for="post in filterBy(orderBy(posts, sortAttribute, -1), searchTerm)" v-bind:key="post.id">
      <h3>Title: {{ post.title }}</h3>
      <img :src="post.image" alt="" />
      <p>Body: {{ post.body }}</p>
      <router-link :to="`/posts/${post.id}`">More Information</router-link>
      <p>Created {{ relativeDate(post.created_at) }}</p>
      <br />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import moment from "moment";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function () {
    return {
      posts: [],
      searchTerm: "",
      sortAttribute: "",
    };
  },
  created: function () {
    axios.get("/posts").then((response) => {
      console.log("Posts array", response.data);
      this.posts = response.data;
    });
  },

  methods: {
    relativeDate: function (date) {
      return moment(date).fromNow();
    },
    setSortAttribute: function (attribute) {
      this.sortAttribute = attribute;
    },
  },
};
</script>
