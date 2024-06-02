<template>
  <div class="video-item card h-100">
    <div class="card-body">
      <h5 class="card-title">{{ video.title }}</h5>
      <p class="card-text"><strong>Tipo:</strong> {{ video.danceType.join(", ") }}</p>
      <p class="card-text"><strong>Tipo lección:</strong> {{ video.lessonType }}</p>
      <p class="card-text"><strong>Fecha:</strong> {{ new Date(video.date).toLocaleDateString() }}</p>
      <p class="card-text"><strong>Profesores:</strong> {{ video.teachers.join(", ") }}</p>
      <p class="card-text"><strong>Nivel:</strong> {{ video.level }}</p>
      <a :href="video.url" target="_blank">Ver Video</a>
      <!-- <a :href="`/watch/${video.id}`" class="btn btn-primary" target="_blank">Ver Video</a> -->
    </div>
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
  margin-bottom: 20px;
}
</style>
