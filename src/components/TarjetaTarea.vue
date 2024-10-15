<script setup>
// importamos la función defineProps de Vue, que se utiliza en el script setup para definir las propiedades (props) que el componente recibe del componente padre
import {defineProps} from 'vue';
// en props vamos a definir las propiedades que nuestro componente va a recibir del padre, asi le estamos diciendo que va a recibir una propiedad tarea que es un tipo objeto y que es obligatoria, tarea es la información que el componente padre pasa al componente hijo para que muestre los detalles de una tarea específica. La información que contiene tarea se define en el componente padre
const props = defineProps({
  tarea: {
    type: Object,
    required: true
  }
  

});
// hay que definir el emit que se propaga del componente al padre en una variable y que usaremos más adelante
const emit = defineEmits(['eliminarTarea']);
</script>



<template>
  <div class="tarjeta-tarea">
    <!-- con el input de tipo checkbox vamos a marcar las tareas completadas, usamos la directiva vmodel para que enlace el valor del checkbox con la propiedad completada de la tarea, bidireccionamente, así cuando marcamos el checkbox el valora de tarea.completada va a cambiar automáticamente -->
    <input type="checkbox" v-model="tarea.completada"/>
    <!-- la directiva v-bind:class asigna la clase completada si tarea completada es true si no lo es, no se añadirá -->
    <span :class="{ completada: tarea.completada }">{{ tarea.nombre }}</span>
    <!-- $emit('eliminar-tarea', tarea) es un moetodo de vue que emite un evento personalizado llamado eliminar-tarea, enviando el de la tarea actual como argumento. Con el dolar($) definimos que es un metodo propio del framework vue y no una propiedad o metodo q hayamos definido nosotros, si no usáramos el $ vue intentaría encontrar un método en mi script llamado emit. Este evento será capturado por el componente padre, que manejará la lógica de eliminación de la tarea y asignará a este evento la funcion eliminarTarea. -->
    <button @click="$emit('eliminarTarea', tarea.id)">ELIMINAR</button>
    <!-- si tarea.imagenUrl existe, se añade por directiva el atributo src con la url recibida del dom  -->
    <img v-if="tarea.imagen" :src="tarea.imagen" alt="Imagen de la tarea" class="imagen-tarea" />
  </div>
</template>



<style scoped>
/* *{
  border: 1px solid red;
} */
/* Estilos para el contenedor principal de la tarjeta */
.tarjeta-tarea {
  border: 1px solid #ccc;
  padding: 10px;
  margin: 10px 50px;
  border-radius: 5px;
  display: flex;
  justify-content:space-around; /* Distribuye los elementos */
  align-items:center; /* Alinea verticalmente */
}

/* Checkbox a la izquierda */
input[type="checkbox"] {
  margin-right: 10px;
}

/* Nombre de la tarea en el centro */
span {
  flex-grow: 1; /* Deja que el nombre ocupe el espacio restante */
  margin: 0 20px;
  white-space: nowrap; /* Evita que el texto salte de línea */
  overflow: hidden;
  text-overflow: ellipsis;
}

/* Estilo para cuando la tarea está completada */
span.completada {
  text-decoration: line-through;
  color: red;
}

/* Estilo para el botón de eliminar */
button {
  background-color: #ff4d4d;
  border: none;
  color: white;
  padding: 5px 10px;
  border-radius: 5px;
  cursor: pointer;
}

button:hover {
  background-color: #cc0000;
}

/* Imagen de la tarea a la derecha */
img {
  max-width: 50px;
  max-height: 50px;
  margin-left: 10px;
}
</style>
