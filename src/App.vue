<template>
  <div class="grid">
    <div class="player">
      <VideoPlayer @prevVideo="prevVideo" @nextVideo="nextVideo" :videosrc="currentVideo"/>
    </div>

    <div class="messages">
      <VideoDetails :title="currentTitle"/> 
      <Chat :messages="messages"/> <!-- Gebruik de Chat component -->
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref, reactive } from 'vue';
import VideoPlayer from './components/Video/VideoPlayer.vue';
import VideoDetails from './components/Video/VideoDetails.vue';
import Chat from './components/Chat/Chat.vue';

const currentTitle = ref('some title here');
const currentVideo = ref('');
const videos = reactive([]);
const currentVideoIndex = ref(0);

onMounted(() => {
  fetch('https://api.jsonbin.io/v3/b/670ccbfaad19ca34f8b81951')
    .then(response => response.json())
    .then(data => {
      videos.value = data.record.data.videos;
      currentVideo.value = videos.value[0].video;
      currentTitle.value = videos.value[0].description;
    });
});

// Video management functions here...
</script>

<style scoped>
.grid {
  font-family: Helvetica;
  display: grid;
  grid-template-columns: 3fr 2fr;
  gap: 1rem;
}

.messages {
  display: flex;
  flex-direction: column;
}
</style>
