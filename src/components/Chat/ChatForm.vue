<script setup>
import { ref, reactive } from 'vue';
import { postMessage } from '../api'; // Zorg ervoor dat dit de juiste pad is

// Gebruik een reactive object voor de nieuwe boodschap
const newMessage = reactive({
  user: 'Wesley', // Hardcodeer de naam naar "Wesley"
  text: ''
});

// Functie om een bericht te plaatsen
const postMessage = async () => {
  if (!newMessage.text) return; // Zorg ervoor dat er tekst is
  try {
    await postMessage(newMessage.user, newMessage.text); // Gebruik de hardcoded naam
    newMessage.text = ''; // Maak het tekstveld leeg na het versturen
  } catch (error) {
    console.error('Error posting message:', error);
  }
};
</script>

<template>
  <div class="form">
    <div>
      <!-- Verwijder de invoer voor de naam -->
      <input v-model="newMessage.text" placeholder="Your message" />
      <button @click="postMessage">Sendd</button>
    </div>
  </div>
</template>

<style scoped>
/* Voeg hier je CSS toe als dat nodig is */
</style>
