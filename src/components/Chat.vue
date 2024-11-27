<template>
    <div class="chat-container">
      <h2>Chat</h2>
      <div class="messages">
        <div
          class="message"
          v-for="(message, index) in messages"
          :key="index"
          :class="getMessageClass(message.owner)"
        >
          <strong>{{ message.owner }}:</strong>
          <p>{{ message.text }}</p>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { defineProps } from 'vue';
  
  // Recibe los mensajes como una prop
  const props = defineProps({
    messages: {
      type: Array,
      required: true
    }
  });
  
  // Función para asignar clases basadas en el nombre del propietario
  const getMessageClass = (owner) => {
    // Aquí se asignan diferentes clases CSS basadas en el propietario
    switch (owner) {
      case 'Persona1':
        return 'persona1-message'; // Clase para Persona1
      case 'Persona2':
        return 'persona2-message'; // Clase para Persona2
      default:
        return 'default-message';  // Clase para mensajes sin dueño específico
    }
  };
  </script>
  
  <style scoped>
  .chat-container {
    border: 1px solid #ccc;
    padding: 20px;
    border-radius: 10px;
    max-width: 400px;
    margin: 0 auto;
  }
  
  .messages {
    max-height: 300px;
    overflow-y: auto;
  }
  
  .message {
    margin-bottom: 10px;
    padding: 10px;
    border-radius: 8px;
    color: #fff; /* El texto dentro del mensaje será blanco */
  }
  
  .persona1-message {
    background-color: #f4a261; /* Naranja para Persona1 */
  }
  
  .persona2-message {
    background-color: #2a9d8f; /* Verde para Persona2 */
  }
  
  .default-message {
    background-color: #dddddd; /* Gris para mensajes sin propietario */
  }
  
  strong {
    font-weight: bold;
  }
  
  p {
    margin: 5px 0;
  }
  </style>
  