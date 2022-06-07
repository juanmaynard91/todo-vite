<template>
  <li class="list-group-item d-flex justify-content-between aling-item-center">
    <span role="button">{{ contar }} Tareas sin hacer</span>
    <span role="button" @click="eliminarCompletados">Eliminar completados</span>
  </li>
</template>

<script setup>
import { computed, inject } from "vue";

const tareas = inject("tareas");

const contar = computed(() => {
  // computed SIEMPRE RETORNA YYYYYYYY NO SON FUNCIONES ASI QUE NO LO PUEDO USAR COMO BOTON
  return tareas.value.filter((el) => el.estado === false).length;
});

const eliminarCompletados = () => {
  tareas.value = tareas.value.filter((el) => el.estado === false); // si es true borra todo menos los completados
};
</script>

<style>
</style>