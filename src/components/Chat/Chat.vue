<!-- Chat.vue -->
<script setup>
import { ref, reactive, onMounted } from 'vue';
import ChatMessages from './ChatMessages.vue';
import ChatForm from './ChatForm.vue';

const messages = reactive([]);

// Fetch messages from the API on component mount
onMounted(() => {
  fetch('https://challenge4-9b1t.onrender.com/api/v1/messages')
    .then(response => response.json())
    .then(data => {
      messages.push(...data.data.messages); // Populate the messages array
    })
    .catch(error => {
      console.error('Error fetching messages:', error);
    });
});

function addMessage(newMessage) {
  messages.unshift(newMessage); // Add to the top of local messages array

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
