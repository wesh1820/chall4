<template>
  <div class="grid">
    <div class="player">
      <VideoPlayer @prevVideo="prevVideo" @nextVideo="nextVideo" :videosrc="currentVideo"/>
    </div>

    <div class="messages">
      <VideoDetails :title="currentTitle"/> 
      <Chat :messages="messages"/>

      <form @submit.prevent="postMessage">
        <input v-model="newMessage" type="text" placeholder="Type your message" required />
        <button type="submit">Send</button>
      </form>
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
const newMessage = ref('');
const messages = reactive([]); // Array to store chat messages

onMounted(() => {
  fetch('https://api.jsonbin.io/v3/b/670ccbfaad19ca34f8b81951')
    .then(response => response.json())
    .then(data => {
      videos.value = data.record.data.videos;
      currentVideo.value = data.record.data.videos[0].video;
      currentTitle.value = data.record.data.videos[0].description;
    });
});

function nextVideo() {
  currentVideoIndex.value++;
  if (currentVideoIndex.value >= videos.value.length) {
    currentVideoIndex.value = 0;
  }
  currentVideo.value = videos.value[currentVideoIndex.value].video;
  currentTitle.value = videos.value[currentVideoIndex.value].description;
}

function prevVideo() {
  currentVideoIndex.value--;
  if (currentVideoIndex.value < 0) {
    currentVideoIndex.value = videos.value.length - 1;
  }
  currentVideo.value = videos.value[currentVideoIndex.value].video;
  currentTitle.value = videos.value[currentVideoIndex.value].description;
}

function postMessage() {
  const messageData = {
    message: newMessage.value,
    timestamp: new Date().toISOString(),
  };

  console.log('Posting message:', messageData); // Log the message being sent

  fetch('YOUR_API_ENDPOINT', { // Replace with your API endpoint
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify(messageData),
  })
    .then(response => {
      if (!response.ok) {
        throw new Error('Network response was not ok');
      }
      return response.json();
    })
    .then(data => {
      messages.push(messageData); // Add to local messages array
      console.log('Message posted successfully:', data);
      newMessage.value = ''; // Clear input after submission
    })
    .catch(error => {
      console.error('There was a problem with the fetch operation:', error);
    });
}
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

form {
  display: flex;
  margin-top: 1rem;
}

input {
  flex: 1;
  margin-right: 0.5rem;
  padding: 0.5rem;
}

button {
  padding: 0.5rem;
}
</style>
