<template>
  <div class="logout"></div>
</template>

<script>
import axios from "axios";

export default {
  created: function () {
    delete axios.defaults.headers.common["Authorization"];
    localStorage.removeItem("jwt");
    this.$parent.flashMessage = "Successfully Logged Out";
    this.$router.push("/");
  }
};
</script>
