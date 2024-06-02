<template>
  <div id="main">
    <h1>Dance Lesson Video Library</h1>
    <MainVideoLibrary />
  </div>
</template>

<script>
import MainVideoLibrary from './components/MainVideoLibrary.vue';

export default {
  name: 'App',
  components: {
    MainVideoLibrary
  }
};
</script>

<style src="./assets/main.css"></style>
