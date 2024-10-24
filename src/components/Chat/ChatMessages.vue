<script setup>
import { onMounted, reactive } from 'vue';

const messages = reactive([]);

// Reactive object for the new message input
const newMessage = reactive({
  user: '',
  text: ''
});

onMounted(() => {
  fetch('https://challenge4-9b1t.onrender.com/api/v1/messages')
    .then(response => response.json())
    .then(data => {
      messages.push(...data.data.messages);
    });
});

// Function to post a new message to the API
const postMessage = () => {
  fetch('https://challenge4-9b1t.onrender.com/api/v1/messages', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(newMessage)
  })
    .then(response => response.json())
    .then(data => {
      if (data.success) {
        messages.push(newMessage); // Add the new message to the list
        newMessage.user = ''; // Clear the user input
        newMessage.text = ''; // Clear the text input
      } else {
        console.error('Error posting message:', data.message);
      }
    })
    .catch(error => console.error('Error:', error));
};
</script>

<template>
  <h2>Comments</h2>
  <ul>
    <li v-for="message in messages" :key="message.id"> <!-- Assuming 'id' is a unique identifier -->
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
