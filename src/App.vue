<template>
  <div id="app">
    <nav class="navbar navbar-light" style="background-color: #e3f2fd;">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">Navbar</a>
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarNav"
          aria-controls="navbarNav"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav">
            <li class="nav-item">
              <router-link class="nav-link" to="/">Home</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" to="/posts">Posts</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" to="/posts/new">New Post</router-link>
            </li>
            <li v-if="isLoggedIn()" class="nav-item">
              <router-link class="nav-link" to="/logout">Logout</router-link>
            </li>
            <li v-if="!isLoggedIn()" class="nav-item">
              <router-link class="nav-link" to="/signup">Signup</router-link>
            </li>
            <li v-if="!isLoggedIn()" class="nav-item">
              <router-link class="nav-link" to="/login">Login</router-link>
            </li>
          </ul>
        </div>
      </div>
    </nav>

    <div v-if="flashMessage">
      {{ flashMessage }}
      <br />
      <button v-on:click="flashMessage = ''">Dismiss</button>
    </div>
    <router-view />
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      flashMessage: "",
    };
  },

  created: function () {},

  methods: {
    isLoggedIn: function () {
      return localStorage.getItem("jwt");
    },
  },
};
</script>
