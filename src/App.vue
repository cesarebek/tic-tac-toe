<template>
  <div id="app">
    <game />
  </div>
</template>

<script>
import Game from './components/Game.vue';
export default {
  name: 'App',
  components: { Game },
};
</script>

<style>
body {
  height: 100vh;
}

body {
  margin: 0;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', 'Oxygen',
    'Ubuntu', 'Cantarell', 'Fira Sans', 'Droid Sans', 'Helvetica Neue',
    sans-serif;
}
</style>
