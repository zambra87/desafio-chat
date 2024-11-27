<script setup>
import { ref } from "vue";
import Persona1 from "./components/Persona1.vue";
import Persona2 from "./components/Persona2.vue";
import Chat from "./components/Chat.vue";

// Estado para almacenar los mensajes
const messages = ref([]);

// Función para agregar el mensaje recibido
const addMessage = (message) => {
  messages.value.push(message);
};

const sendText = () => {
  if (message.value.trim() !== '') {
    // Emitir mensaje con el nombre de la persona y el texto
    emit('sendMessage', { owner: `${personas.value[0]?.name.first} ${personas.value[0]?.name.last}`, text: message.value });
    message.value = ''; // Limpiar el campo de texto después de enviar
  }
};
</script>

<template>
  <div class="grid-container">
    <!-- Pasar la función addMessage a los componentes Persona1 y Persona2 -->
    <Persona1 @sendMessage="addMessage" />
    <Chat :messages="messages" />
    <Persona2 @sendMessage="addMessage" />
  </div>
</template>

<style scoped>
.grid-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr); /* 3 columnas */
  gap: 16px;
}

.grid-container > * {
  background-color: #f4f4f4;
  padding: 16px;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}
</style>
