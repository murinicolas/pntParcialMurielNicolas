<template>
  <div id="app" class="container-fluid mt-3">
    <div class="jumbotron" style="background-color: #a0e2ff">
      <h1>Primer parcial</h1>
      <br>
      <Navbar />
      <router-view></router-view>

    </div>
  </div>
</template>

<script>

import Navbar from './componentes/Navbar.vue'
export default {
  name: 'App',
  components: {
    Navbar
  }
}
</script>

<style>
#app {
}

h1 {
  color: white;
}
</style>
