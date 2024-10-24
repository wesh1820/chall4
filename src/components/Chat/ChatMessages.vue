<script setup>
import { onMounted, reactive } from 'vue';

// Reactive state voor berichten en nieuwe berichten
const messages = reactive([]);
const newMessage = reactive({ user: '', text: '' });

// Functie om berichten van de API te halen
onMounted(() => {
  fetch('https://les3.onrender.com/api/v1/messages')
    .then(response => response.json())
    .then(data => {
      messages.push(...data.data.messages);
    });
});

// Functie om een nieuw bericht te versturen
const postMessage = () => {
  fetch('https://les3.onrender.com/api/v1/messages', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify(newMessage),
  })
    .then(response => response.json())
    .then(data => {
      // Voeg het nieuwe bericht toe aan de lijst en reset het formulier
      messages.push(data.data.message);
      newMessage.user = 'Wesley';
      newMessage.text = '';
    })
    .catch(error => console.error('Error:', error));
};
</script>

<template>
  <h2>Comments</h2>
  <ul>
    <li v-for="message in messages" :key="message.id">
      <strong>{{ message.user }}</strong>: {{ message.text }}
    </li>
  </ul>

  <!-- Formulier om een nieuw bericht toe te voegen -->
  <div>
    <input v-model="newMessage.user" placeholder="Your name" />
    <input v-model="newMessage.text" placeholder="Your message" />
    <button @click="postMessage">Send</button>
  </div>
</template>

<style scoped>
/* Voeg hier je stijlen toe */
</style>
