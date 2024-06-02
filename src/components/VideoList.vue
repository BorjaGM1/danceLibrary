<template>
  <div class="container">
    <div class="row">
      <div class="col-md-3">
        <VideoFilters :filters="filters" @applyFilters="applyFilters" />
      </div>
      <div class="col-md-9">
        <div class="row mb-3">
          <div class="col-12">
            <input 
              v-model="filters.title" 
              @input="applyFilters(filters)" 
              class="form-control" 
              placeholder="Search by title"
            />
          </div>
        </div>
        <div class="row">
          <div v-if="filteredVideos.length">
            <div class="col-md-4" v-for="video in filteredVideos" :key="video.title">
              <VideoItem :video="video" />
            </div>
          </div>
          <div v-else>
            <p>No videos found.</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import VideoItem from './VideoItem.vue';
import VideoFilters from './VideoFilters.vue';
import videos from '../data/videos.json';

export default {
  name: 'VideoList',
  components: { VideoItem, VideoFilters },
  data() {
    return {
      videos: videos,
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
        const matchesLevel = !filters.levels.length || filters.levels.includes(video.level);
        return matchesTitle && matchesDateRange && matchesDanceType && matchesLessonType && matchesTeachers && matchesLevel;
      });
    }
  }
};
</script>

<style scoped>
.container {
  padding-top: 20px;
}
</style>
