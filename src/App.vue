<template>
  <div id="app">
    <google-login></google-login>
  </div>
</template>

<script>
import GoogleLogin from "./views/GoogleLogin";
export default {
  name: "App",
  components: {
    GoogleLogin,
  },
};
</script>

<style>
body {
  margin: 0;
  font-family: "Roboto", "sans-serif";
  background-color: #cdd3e1;
}
</style>
