<template>
  <div id="app" class="container">
    <SearchBar @termChange="onTermChanged"></SearchBar>
    <div class="row">
    <VideoDetail :video="selectedVideo"></VideoDetail>
    <VideoList @videoSelect="onVideoSelect" :videos="videos"></VideoList>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import SearchBar from './components/SearchBar.vue';
import VideoList from './components/VideoList'
import VideoDetail from './components/VideoDetail'
const API_KEY = <API_KEY>;

export default {
  name: 'App',
  components: {
    SearchBar,
    VideoList,
    VideoDetail
  },
  data(){
    return {videos: [], selectedVideo: null};
  },
  methods:{
    onVideoSelect(video){
      this.selectedVideo = video;
    },
    onTermChanged(searchTerm){
      axios.get('https://www.googleapis.com/youtube/v3/search',{
        params: {
          key: API_KEY,
          type: 'video',
          part:'snippet',
          q: searchTerm
        }
      }).then(response => {
        console.log(response.data.items)
        this.videos = response.data.items
      });
    }
  }
}
</script>

<style>

</style>
