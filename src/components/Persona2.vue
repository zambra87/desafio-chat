<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";

// Declarar el estado reactivo
const personas = ref([]);
const message = ref("");  // Estado para el mensaje que se enviará

// Función para obtener datos de la API
const getPersona = async () => {
  try {
    const url = "https://randomuser.me/api/";
    const { data } = await axios.get(url);
    personas.value = data.results; // Actualizar el estado reactivo con la persona obtenida
  } catch (error) {
    console.error(error);
  }
};

// Llamar a la función al montar el componente
onMounted(() => {
  getPersona();
});

// Emitir el mensaje al componente padre
const emit = defineEmits(['sendMessage']); // Emitir un evento 'sendMessage' al componente padre

// Función para enviar el mensaje
const sendText = () => {
  if (message.value.trim() !== '') {
    // Emitir mensaje con el nombre de la persona y el texto
    emit('sendMessage', { owner: `${personas.value[0]?.name.first} ${personas.value[0]?.name.last}`, text: message.value });
    message.value = ''; // Limpiar el campo de texto después de enviar
  }
};
</script>

<template>
  <div>
    <ul>
      <li v-for="persona in personas" :key="persona.email">
        <img :src="persona.picture.large" :alt="`${persona.name.first} ${persona.name.last}`" />
        <p>{{ persona.name.first }} {{ persona.name.last }}</p>
      </li>
    </ul>
    <div class="input-container">
      <label for="textInput">Escribe algo:</label>
      <input v-model="message" type="text" id="textInput" placeholder="Escribe aquí..." />
      <button @click="sendText">Enviar</button>
    </div>
  </div>
</template>

<style scoped>
/* Puedes agregar aquí los estilos si los necesitas */
</style>