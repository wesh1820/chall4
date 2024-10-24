<!-- Chat.vue -->
<script setup>
import { ref, reactive } from 'vue';
import ChatMessages from './ChatMessages.vue';
import ChatForm from './ChatForm.vue';

const messages = reactive([]); // Array to hold messages

function addMessage(newMessage) {
  messages.push(newMessage);
}

</script>

<template>
  <ChatMessages :messages="messages" />
  <ChatForm @sendMessage="addMessage" />
</template>

<style scoped>
/* Add any styles for your Chat component here */
</style>
