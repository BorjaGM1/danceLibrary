<template>
  <div class="video-item">
    <h2>{{ video.title }}</h2>
    <p><strong>Tipo:</strong> {{ video.danceType.join(", ") }}</p>
    <p><strong>Tipo lección:</strong> {{ video.lessonType }}</p>
    <p><strong>Fecha:</strong> {{ new Date(video.date).toLocaleDateString() }}</p>
    <p><strong>Profesores:</strong> {{ video.teachers.join(", ") }}</p>
    <p><strong>Nivel:</strong> {{ video.level }}</p>
    <a :href="video.url" target="_blank">Ver Video</a>
  </div>
</template>

<script>
export default {
  name: 'VideoItem',
  props: {
    video: Object
  }
};
</script>

<style scoped>
.video-item {
  border: 1px solid #ccc;
  padding: 10px;
  margin: 10px 0;
}
</style>