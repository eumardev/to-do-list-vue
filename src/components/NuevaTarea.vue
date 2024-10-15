
<!-- nuevo componente NuevaTarea que controla la funcionalidad crearTarea -->
<script setup>
import { ref } from 'vue';

// Define emit para poder emitir eventos al componente padre
const emit = defineEmits(['crearTarea']);


const nuevaTarea = ref('');
const imagenURL = ref('');
let id = 0;

// Crear y Emitir la tarea creada al componente padre para que lo agregue al array de tareas
const crearTarea = () => {
  if (nuevaTarea.value.trim()) {
    // Emitimos la tarea nueva hacia el componente padre
    const tarea = {
      id: id++,
      nombre: nuevaTarea.value,
      imagen: imagenURL.value || '../public/img/imagenPorDefecto.jpg',
      completada: false,
    };
    // Emitir evento 'crear-tarea' al componente padre para que lo agregue al array de tareas
    emit('crearTarea', tarea);

    // Limpiar los campos de entrada
    nuevaTarea.value = '';
    imagenURL.value = '';
  }
};
</script>

<template>
  <form @submit.prevent="crearTarea">
    <input v-model="nuevaTarea" placeholder="Introduce una tarea" required>
    <input v-model="imagenURL" placeholder="URL de la imagen (opcional)">
    <button>Crear una tarea</button>
  </form>
</template>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-bottom: 20px;
}
input, button {
  padding: 10px;
  border-radius: 5px;
  border: 1px solid #ccc;
  font-size: 16px;
}
button {
  background-color: lightgray;
  cursor: pointer;
}
button:hover {
  background-color: grey;
  color: white;
}
</style>
