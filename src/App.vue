<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
  <MyChat />
</template>

<script>
import MyChat from './components/MyChat.vue'

export default {
  name: 'App',
  components: {
    MyChat,
  },
}
</script>

<style>
html,
body,
#app {
  height: 100%;
  margin: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #000;
}
</style>
