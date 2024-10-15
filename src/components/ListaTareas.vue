
<script setup>
import { ref, computed, defineProps } from 'vue';
import TarjetaTarea from './TarjetaTarea.vue';

const emit = defineEmits(['eliminarTarea']);

// Definir las propiedades que se reciben desde App.vue
const props = defineProps({
  tareas: {
    type: Array,
    required: true
  }
});

// Variable reactiva para controlar si se ocultan las tareas completadas
const ocultar = ref(false);

// Computada para filtrar las tareas
const tareasFiltradas = computed(() => {
  return ocultar.value
    ? props.tareas.filter(tarea => !tarea.completada)
    : props.tareas;
});

// Función para alternar el filtro de tareas completadas
const toggleOcultar = () => {
  ocultar.value = !ocultar.value;
};

</script>

<template>
  <!-- Listado de tareas filtradas, tenemos que definir el posible evento eliminarTarea  que puede venir de tarjetaTarea-->
  <div class="divTareas">
    <tarjetaTarea
      v-for="tarea in tareasFiltradas"
      :key="tarea.id"
      :tarea="tarea"
      @eliminarTarea="$emit('eliminarTarea', tarea.id)"
    />
  </div>

  <!-- Botón para alternar entre mostrar todas o solo pendientes -->
  <button @click="toggleOcultar">{{ ocultar ? 'Ver todas las tareas' : 'Ver solo tareas pendientes' }}
  </button>
</template>




<style scoped>
.divTareas {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

button {
  margin: 10px 50px;
  padding: 10px;
  background-color: lightgray;
  cursor: pointer;
}

button:hover {
  background-color: grey;
  color: white;
}
</style>
