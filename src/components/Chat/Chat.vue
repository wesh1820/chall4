<!-- Chat.vue -->
<script setup>
import { ref, reactive } from 'vue';
import ChatMessages from './ChatMessages.vue';
import ChatForm from './ChatForm.vue';

const messages = reactive([]);

function addMessage(newMessage) {
  messages.push(newMessage); // Add to local messages array

  // Send the new message to the API
  fetch('https://challenge4-9b1t.onrender.com/api/v1/messages', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify(newMessage),
  })
  .then(response => response.json())
  .then(data => {
    console.log('Message posted successfully:', data);
  })
  .catch(error => {
    console.error('Error posting message:', error);
  });
}
</script>

<template>
  <ChatMessages :messages="messages" />
  <ChatForm @sendMessage="addMessage" />
</template>

<style scoped>
/* Add any styles for your Chat component here */
</style>
