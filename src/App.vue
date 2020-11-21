<template>
  <AppHome />
</template>

<script>
import AppHome from "@/views/AppHome.vue";
export default {
  name: "App",
  components: {
    AppHome,
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}

html,
body {
  height: 100%;
  margin: 0;
  padding: 0;
}

body {
  font-family: sans-serif;
  padding-top: 3rem;
}
</style>
