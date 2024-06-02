<template>
  <div class="filters">
    <div class="filter-row">
      <div class="filter-section">
        <label for="search-title">Buscar por nombre</label>
        <input id="search-title" v-model="filters.title" @input="updateFilters" placeholder="Search by title" />
      </div>

      <div class="filter-section">
        <label for="start-date">Fecha Inicio</label>
        <input id="start-date" type="date" v-model="filters.dateRange.start" @change="updateFilters" />
      </div>

      <div class="filter-section">
        <label for="end-date">Fecha Fin</label>
        <input id="end-date" type="date" v-model="filters.dateRange.end" @change="updateFilters" />
      </div>
    </div>

    <div class="filter-row">
      <div class="filter-section">
        <h3>Tipo</h3>
        <div v-for="type in uniqueDanceTypes" :key="type">
          <input type="checkbox" :value="type" v-model="filters.danceTypes" @change="updateFilters" /> {{ type }}
        </div>
      </div>

      <div class="filter-section">
        <h3>Tipo lección</h3>
        <div v-for="type in uniqueLessonTypes" :key="type">
          <input type="checkbox" :value="type" v-model="filters.lessonTypes" @change="updateFilters" /> {{ type }}
        </div>
      </div>

      <div class="filter-section">
        <h3>Profesores</h3>
        <select v-model="filters.teachers" @change="updateFilters" multiple>
          <option v-for="teacher in uniqueTeachers" :key="teacher" :value="teacher">{{ teacher }}</option>
        </select>
      </div>
    </div>

    <div class="filter-row">
      <div class="filter-section">
        <h3>Nivel</h3>
        <div v-for="level in uniqueLevels" :key="level">
          <input type="checkbox" :value="level" v-model="filters.levels" @change="updateFilters" /> {{ level }}
        </div>
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
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.filter-row {
  display: flex;
  gap: 20px;
  flex-wrap: wrap;
}

.filter-section {
  flex: 1;
  min-width: 200px;
}

.filter-section h3 {
  margin: 0;
}

.filter-section label {
  display: block;
  margin-bottom: 5px;
}

.filter-section select {
  width: 100%;
  height: 100px;
}
</style>
