<template>
  <div id="q-app">
<!--    <router-view />-->
    <index></index>
  </div>
</template>

<script>
  import Index from './pages/Index.vue'
export default {
  name: 'App',
    components: {
      Index
    }
}
</script>

<style>
  body {
    height: 100vh;
    width: 100vw;
  }

  #q-app {
    height: 100vh;
    width: 100vw;
  }
</style>
