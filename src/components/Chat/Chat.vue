<!-- src/components/Chat.vue -->
<template>
  <ChatMessages :messages="messages" />
  <ChatForm @sendMessage="addMessage" />
</template>

<script setup>
import { reactive, onMounted } from 'vue';
import ChatMessages from './ChatMessages.vue';
import ChatForm from './ChatForm.vue';

const messages = reactive([]);

// Fetch messages from the API on component mount
onMounted(() => {
  fetch('https://challenge4-9b1t.onrender.com/api/v1/messages')
    .then(response => {
      if (!response.ok) {
        throw new Error(`HTTP error! status: ${response.status}`);
      }
      return response.json();
    })
    .then(data => {
      messages.push(...data.data.messages); // Populate the messages array
    })
    .catch(error => {
      console.error('Error fetching messages:', error);
    });
});

// Function to add a new message
function addMessage(newMessage) {
  messages.unshift(newMessage); // Add to the top of local messages array

  // Construct payload for the API
  const payload = {
    user: newMessage.user, // Ensure this matches API's expectations
    text: newMessage.text,
  };

  // Send the new message to the API
  fetch('https://challenge4-9b1t.onrender.com/api/v1/messages', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify(payload),
  })
    .then(response => {
      if (!response.ok) {
        throw new Error(`HTTP error! status: ${response.status}`);
      }
      return response.json();
    })
    .then(data => {
      console.log('Message posted successfully:', data);
    })
    .catch(error => {
      console.error('Error posting message:', error);
    });
}
</script>

<style scoped>
/* Add any styles for your Chat component here */
</style>
