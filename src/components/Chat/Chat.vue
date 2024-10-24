<script setup>
import ChatMessages from './ChatMessages.vue';
import ChatForm from './ChatForm.vue';
import { reactive } from 'vue';

const messages = reactive([]);

// Functie om berichten op te halen
async function fetchMessages() {
  const response = await fetch('https://challenge4-9b1t.onrender.com');
  const data = await response.json();
  messages.push(...data.data.messages);
}

// Functie om een bericht toe te voegen
function addMessage(message) {
  messages.unshift(message); // Voeg het bericht aan de bovenkant toe
}

// Ophalen van berichten bij het laden van de component
fetchMessages();
</script>

<template>
  <ChatMessages :messages="messages" />
  <ChatForm @messageSent="addMessage" />
</template>

<style scoped>
/* Voeg styling toe indien nodig */
</style>
