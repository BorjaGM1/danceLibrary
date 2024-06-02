<template>
  <div class="filters">
    <div class="form-group">
      <label for="search-title">Buscar por nombre</label>
      <input id="search-title" v-model="filters.title" @input="updateFilters" class="form-control" placeholder="Search by title" />
    </div>
    <div class="form-group">
      <label for="start-date">Fecha Inicio</label>
      <input id="start-date" type="date" v-model="filters.dateRange.start" @change="updateFilters" class="form-control" />
    </div>
    <div class="form-group">
      <label for="end-date">Fecha Fin</label>
      <input id="end-date" type="date" v-model="filters.dateRange.end" @change="updateFilters" class="form-control" />
    </div>
    <div class="form-group">
      <h5>Tipo</h5>
      <div v-for="type in uniqueDanceTypes" :key="type" class="form-check">
        <input type="checkbox" :value="type" v-model="filters.danceTypes" @change="updateFilters" class="form-check-input" /> 
        <label class="form-check-label">{{ type }}</label>
      </div>
    </div>
    <div class="form-group">
      <h5>Tipo lección</h5>
      <div v-for="type in uniqueLessonTypes" :key="type" class="form-check">
        <input type="checkbox" :value="type" v-model="filters.lessonTypes" @change="updateFilters" class="form-check-input" /> 
        <label class="form-check-label">{{ type }}</label>
      </div>
    </div>
    <div class="form-group">
      <h5>Profesores</h5>
      <select v-model="filters.teachers" @change="updateFilters" class="form-control" multiple>
        <option v-for="teacher in uniqueTeachers" :key="teacher" :value="teacher">{{ teacher }}</option>
      </select>
    </div>
    <div class="form-group">
      <h5>Nivel</h5>
      <div v-for="level in uniqueLevels" :key="level" class="form-check">
        <input type="checkbox" :value="level" v-model="filters.levels" @change="updateFilters" class="form-check-input" /> 
        <label class="form-check-label">{{ level }}</label>
      </div>
    </div>
  </div>
</template>

<script>
import videos from '../data/videos.json';

export default {
  name: 'VideoFilters',
  data() {
    return {
      filters: {
        title: '',
        dateRange: {
          start: '',
          end: ''
        },
        danceTypes: [],
        lessonTypes: [],
        teachers: [],
        levels: []
      }
    };
  },
  computed: {
    uniqueDanceTypes() {
      return [...new Set(videos.flatMap(video => video.danceType))];
    },
    uniqueLessonTypes() {
      return [...new Set(videos.map(video => video.lessonType))];
    },
    uniqueTeachers() {
      return [...new Set(videos.flatMap(video => video.teachers))];
    },
    uniqueLevels() {
      return [...new Set(videos.map(video => video.level))];
    }
  },
  methods: {
    updateFilters() {
      this.$emit('applyFilters', this.filters);
    }
  }
};
</script>

<style scoped>
.filters {
  padding: 15px;
  border: 1px solid #ddd;
  border-radius: 4px;
  background-color: #f8f9fa;
}
</style>
