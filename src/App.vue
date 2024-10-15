

<!-- -------------------------------app.vue con solo gestion de array de tareas----------------------------- -->
<script setup>
import { ref } from 'vue';
// defino las importaciones de los componentes hijos
import NuevaTarea from './components/NuevaTarea.vue';
import ListaTareas from './components/ListaTareas.vue';

// Array de tareas
const tareas = ref([]);

// Función para manejar la tarea creada desde el componente NuevaTarea.vue y agregarlo al array que tenemos 
const agregarTareaArray = (nuevaTarea) => {
  tareas.value.push(nuevaTarea);
};

// Función para eliminar la tarea del array
const eliminarTareaArray = (id) => {
  console.log("Eliminando tarea con id:", id);
  tareas.value = tareas.value.filter((t) => t.id !== id);
};
</script>

<template>
  <header>
    <h1>APP DE TAREAS</h1>
  </header>
  <body>  
    <div>
    <h2>Crear nueva tarea</h2>
    <!-- Componente para añadir una nueva tarea -->
    <NuevaTarea @crearTarea="agregarTareaArray" />
    <h2>Listado de tareas</h2>
    <!-- Componente para mostrar la lista de tareas -->
    <ListaTareas :tareas="tareas" @eliminarTarea="eliminarTareaArray" />
  </div>
  </body>

</template>

<style scoped>
body {
  font-family: Arial, sans-serif;
  background-color: #f4f4f4;
  padding: 20px;
}
</style>
