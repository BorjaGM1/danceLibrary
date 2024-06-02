<template>
    <div class="filters">
      <input v-model="filters.title" @input="updateFilters" placeholder="Search by title" />
  
      <input type="date" v-model="filters.dateRange.start" @change="updateFilters" placeholder="Start Date" />
      <input type="date" v-model="filters.dateRange.end" @change="updateFilters" placeholder="End Date" />
  
      <div v-for="type in uniqueDanceTypes" :key="type">
        <input type="checkbox" :value="type" v-model="filters.danceTypes" @change="updateFilters" /> {{ type }}
      </div>
  
      <div v-for="type in uniqueLessonTypes" :key="type">
        <input type="checkbox" :value="type" v-model="filters.lessonTypes" @change="updateFilters" /> {{ type }}
      </div>
  
      <div v-for="teacher in uniqueTeachers" :key="teacher">
        <input type="checkbox" :value="teacher" v-model="filters.teachers" @change="updateFilters" /> {{ teacher }}
      </div>
  
      <div v-for="level in uniqueLevels" :key="level">
        <input type="checkbox" :value="level" v-model="filters.levels" @change="updateFilters" /> {{ level }}
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
        return [...new Set(videos.map(video => video.danceType))];
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
    margin-bottom: 20px;
  }
  </style>
  