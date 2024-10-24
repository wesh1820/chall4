<script setup>
import ChatMessages from './ChatMessages.vue';
import ChatForm from './ChatForm.vue';
import { reactive } from 'vue';

const messages = reactive([]);

// Vervang dit door je eigen API endpoint URL
const API_URL = 'https://challenge4-9b1t.onrender.com/api/v1/messages';

// Functie om berichten op te halen
async function fetchMessages() {
  try {
    const response = await fetch(`${API_URL}/messages`);
    const data = await response.json();
    messages.push(...data.data.messages); // Voeg opgehaalde berichten toe
  } catch (error) {
    console.error('Error fetching messages:', error);
  }
}

// Functie om een bericht toe te voegen en te posten naar de API
async function addMessage(newMessage) {
  try {
    const response = await fetch(`${API_URL}/messages`, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(newMessage),
    });

    if (!response.ok) {
      throw new Error('Failed to post message');
    }

    const data = await response.json();
    messages.unshift(newMessage); // Voeg lokaal het nieuwe bericht toe
  } catch (error) {
    console.error('Error posting message:', error);
  }
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
