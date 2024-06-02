<template>
    <div class="video-item">
      <h3>{{ video.title }}</h3>
      <p>Type: {{ video.danceType }} | Level: {{ video.level }}</p>
      <p>Lesson Type: {{ video.lessonType }} | Date: {{ video.date }}</p>
      <p>Teachers: {{ video.teachers.join(', ') }}</p>
      <a :href="video.url" target="_blank">Watch Video</a>
    </div>
  </template>
  
  <script>
  export default {
    name: 'VideoItem',
    props: {
      video: Object
    }
  }
  </script>
  
  <style scoped>
  .video-item {
    border: 1px solid #ccc;
    padding: 10px;
    margin: 10px 0;
  }
  </style>
  