<!-- ChatForm.vue -->
<template>
  <div class="form">
    <input v-model="messageText" type="text" placeholder="Type your message here" />
    <button @click="sendMessage">Send</button>
  </div>
</template>

<script setup>
import { ref, defineEmits } from 'vue';

const emit = defineEmits();
const messageText = ref('');

function sendMessage() {
  if (messageText.value.trim() !== '') {
    const newMessage = {
      user: 'Your Name', // Replace with actual user name or fetch dynamically
      text: messageText.value,
    };
    emit('sendMessage', newMessage); // Emit the new message to the parent
    messageText.value = ''; // Clear input after sending
  }
}
</script>

<style scoped>
.form {
  display: flex;
  margin-top: 1rem;
}
input {
  flex: 1;
  margin-right: 0.5rem;
  padding: 0.5rem;
}
button {
  padding: 0.5rem;
}
</style>
