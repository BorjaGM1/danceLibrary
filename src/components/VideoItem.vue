<template>
  <div class="video-item card bg-dark text-white mb-3">
    <div class="card-body">
      <h5 class="card-title">{{ video.title }}</h5>
      <p class="card-text"><strong>Tipo:</strong> {{ video.danceType.join(", ") }}</p>
      <p class="card-text"><strong>Tipo lección:</strong> {{ video.lessonType }}</p>
      <p class="card-text"><strong>Fecha:</strong> {{ new Date(video.date).toLocaleDateString() }}</p>
      <p class="card-text"><strong>Profesores:</strong> {{ video.teachers.join(", ") }}</p>
      <p class="card-text"><strong>Nivel:</strong> {{ video.level.join(", ") }}</p>
      <a :href="video.url" target="_blank">Ver En Youtube</a>
      <a :href="`/watch.html?id=${video.id}`" class="btn btn-primary">Ver Aquí</a>
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
  border: 1px solid #1db954;
}
</style>
