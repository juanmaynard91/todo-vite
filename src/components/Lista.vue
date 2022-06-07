<template>
  <ul class="list-group">
    <Items v-for="tarea in tareas" :key="tarea.id" :tarea="tarea" />
    <li class="form-control my-3" v-if="tareas.length === 0">No hay Tareas</li>
    <Footer v-else />
    <Filtro />
  </ul>
</template>

<script setup>
import { computed, inject, provide, ref } from "vue";
import Items from "./Items.vue";
import Footer from "./Footer.vue";
import Filtro from "./Filtro.vue";

const todasLasTareas = inject("tareas");
const estado = ref("Todos"); //por defecto muestro todas las tareas

const tareas = computed(() => { 
  if (estado.value === "Todos") {
    return todasLasTareas.value; //muestro todas las tareas
  }
  if (estado.value === "Activos") {
    return todasLasTareas.value.filter((el) => el.estado === false);
  }
  if (estado.value === "Completados") {
    return todasLasTareas.value.filter((el) => el.estado === true);
  }
});

provide("estado", estado); 
</script>

<style>
</style>