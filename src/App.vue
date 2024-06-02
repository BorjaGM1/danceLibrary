<template>
  <div id="app">
    <h1>Dance Lesson Video Library</h1>
    <VideoList />
  </div>
</template>

<script>
import VideoList from './components/VideoList.vue';

export default {
  name: 'App',
  components: {
    VideoList
  }
};
</script>

<!-- <style src="./styles/main.css"></style> -->
