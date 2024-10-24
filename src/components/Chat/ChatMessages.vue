<script setup>
import { onMounted, reactive } from 'vue';

const messages = reactive([]);
const newMessage = reactive({
  user: '',
  text: ''
});

onMounted(() => {
  fetch('https://challenge4-9b1t.onrender.com/api/v1/messages')
    .then(response => response.json())
    .then(data => {
      messages.push(...data.data.messages);
    })
    .catch(error => console.error('Error fetching messages:', error));
});

const postMessage = () => {
  console.log('Posting message:', newMessage); // Log the message being posted
  fetch('https://challenge4-9b1t.onrender.com/api/v1/messages', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(newMessage)
  })
    .then(response => {
      if (!response.ok) {
        throw new Error('Network response was not ok ' + response.statusText);
      }
      return response.json();
    })
    .then(data => {
      console.log(data); // Log the response for debugging
      if (data.success) {
        messages.push({ ...newMessage });
        newMessage.user = '';
        newMessage.text = '';
      } else {
        console.error('Error posting message:', data.message);
      }
    })
    .catch(error => console.error('Error posting message:', error));
};
</script>

<template>
  <h2>Comments</h2>
  <ul>
    <li v-for="message in messages" :key="message.id">
      <strong>{{ message.user }}</strong>: {{ message.text }}
    </li>
  </ul>
  
  <form @submit.prevent="postMessage">
    <input 
      v-model="newMessage.user" 
      type="text" 
      placeholder="Your Name" 
      required 
    />
    <input 
      v-model="newMessage.text" 
      type="text" 
      placeholder="Your Comment" 
      required 
    />
    <button type="submit">Post Message</button>
  </form>
</template>

<style scoped>
/* Add your styles here */
</style>
