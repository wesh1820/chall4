<script setup>
import { ref } from 'vue';
const messageText = ref('');

function sendMessage() {
  if (messageText.value.trim() === '') return; // Zorg ervoor dat er geen lege berichten worden verzonden

  const newMessage = {
    user: 'Anonymous', // Je kunt de user aanpassen als dat nodig is
    text: messageText.value,
  };

  // Emit het nieuwe bericht naar de oudercomponent
  emit('messageSent', newMessage);

  messageText.value = ''; // Leeg het invoerveld
}
</script>

<template>
  <div class="form">
    <input v-model="messageText" type="text" placeholder="Type your message here" />
    <button @click="sendMessage">Send</button>
  </div>
</template>

<style scoped>
/* Voeg styling toe indien nodig */
</style>
