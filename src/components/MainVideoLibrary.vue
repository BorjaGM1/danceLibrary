<template>
  <div class="container">
    <div class="row">
      <div class="col-md-3">
        <VideoFilters :filters="filters" @applyFilters="applyFilters" />
      </div>
      <div class="col-md-9">
        <input 
          v-model="filters.title" 
          @input="applyFilters(filters)" 
          class="form-control mb-3" 
          placeholder="Search by title"
        />
        <div class="row">
          <VideoItem 
            v-for="video in filteredVideos" 
            :key="video.title" 
            :video="video" 
            class="col-md-4 mb-3"
          />
        </div>
        <div v-if="!filteredVideos.length">
          <p>No videos found.</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import VideoFilters from './VideoFilters.vue';
import VideoItem from './VideoItem.vue';
import videos from '../data/videos.json';

export default {
  name: 'MainVideoLibrary',
  components: {
    VideoFilters,
    VideoItem
  },
  data() {
    return {
      videos,
      filteredVideos: videos,
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
  methods: {
    applyFilters(filters) {
      this.filteredVideos = this.videos.filter(video => {
        const matchesTitle = video.title.toLowerCase().includes(filters.title.toLowerCase());
        const matchesDateRange = (!filters.dateRange.start || new Date(video.date) >= new Date(filters.dateRange.start)) &&
                                 (!filters.dateRange.end || new Date(video.date) <= new Date(filters.dateRange.end));
        const matchesDanceType = !filters.danceTypes.length || filters.danceTypes.some(type => video.danceType.includes(type));
        const matchesLessonType = !filters.lessonTypes.length || filters.lessonTypes.includes(video.lessonType);
        const matchesTeachers = !filters.teachers.length || filters.teachers.some(teacher => video.teachers.includes(teacher));
        const matchesLevel = !filters.levels.length || filters.levels.some(level => video.level.includes(level));
        
        return matchesTitle && matchesDateRange && matchesDanceType && matchesLessonType && matchesTeachers && matchesLevel;
      });
    }
  }
};
</script>

<style scoped>
/* Add styles here if needed */
</style>
