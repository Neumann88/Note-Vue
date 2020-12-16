<template>
  <div class="wrapper">
    <NotesMain/>
  </div>
</template>

<script>
  import NotesMain from './components/NotesMain.vue'

  export default {
    name: 'App',
    components: {
      NotesMain
    }
  }
</script>

<style>
  .wrapper {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    margin-top: 60px;
  }
</style>
