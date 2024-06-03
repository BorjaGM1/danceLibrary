<template>
  <div class="filters bg-dark text-white p-3 rounded">
    <div class="form-group">
      <label for="search-title">Buscar por nombre</label>
      <input id="search-title" v-model="filters.title" @input="updateFilters" class="form-control bg-dark text-white border-secondary" placeholder="Search by title" />
    </div>
    <div class="form-group">
      <label for="start-date">Fecha Inicio</label>
      <input id="start-date" type="date" v-model="filters.dateRange.start" @change="updateFilters" class="form-control bg-dark text-white border-secondary" />
    </div>
    <div class="form-group">
      <label for="end-date">Fecha Fin</label>
      <input id="end-date" type="date" v-model="filters.dateRange.end" @change="updateFilters" class="form-control bg-dark text-white border-secondary" />
    </div>
    <div class="form-group">
      <h5>Tipo</h5>
      <div v-for="type in uniqueDanceTypes" :key="type" class="form-check">
        <input type="checkbox" :value="type" v-model="filters.danceTypes" @change="updateFilters" class="form-check-input" id="danceType-{{type}}" /> 
        <label class="form-check-label" :for="`danceType-${type}`">{{ type }}</label>
      </div>
    </div>
    <div class="form-group">
      <h5>Tipo lección</h5>
      <div v-for="type in uniqueLessonTypes" :key="type" class="form-check">
        <input type="checkbox" :value="type" v-model="filters.lessonTypes" @change="updateFilters" class="form-check-input" id="lessonType-{{type}}" /> 
        <label class="form-check-label" :for="`lessonType-${type}`">{{ type }}</label>
      </div>
    </div>
    <div class="form-group">
      <h5>Profesores</h5>
      <select v-model="filters.teachers" @change="updateFilters" class="form-control select2 bg-dark text-white border-secondary" multiple>
        <option v-for="teacher in uniqueTeachers" :key="teacher" :value="teacher">{{ teacher }}</option>
      </select>
    </div>
    <div class="form-group">
      <h5>Nivel</h5>
      <div v-for="level in uniqueLevels" :key="level" class="form-check">
        <input type="checkbox" :value="level" v-model="filters.levels" @change="updateFilters" class="form-check-input" id="level-{{level}}" /> 
        <label class="form-check-label" :for="`level-${level}`">{{ level }}</label>
      </div>
    </div>
  </div>
</template>

<script>
import videos from '../data/videos.json';
import $ from 'jquery';
import 'select2/dist/css/select2.min.css';
import 'select2/dist/js/select2.min.js';

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
      return [...new Set(videos.flatMap(video => video.level))];
    }
  },
  methods: {
    updateFilters() {
      this.$emit('applyFilters', this.filters);
    }
  },
  mounted() {
    $(this.$el).find('.select2').select2({
      theme: 'bootstrap4',
      width: '100%'
    }).on('change', this.updateFilters);
  }
};
</script>

<style scoped>
.filters {
  padding: 15px;
  border-radius: 4px;
}
</style>
