<template>
  <li class="list-group-item d-flex justify-content-between align-items-center list-group-item-action">
    <span role="button" @click="completado(tarea.id)" :class="{tachado: tarea.estado}">{{ tarea.name }}</span>
    <span role="button" @click="eliminar(tarea.id)">
      <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-x-lg" viewBox="0 0 16 16">
        <path d="M2.146 2.854a.5.5 0 1 1 .708-.708L8 7.293l5.146-5.147a.5.5 0 0 1 .708.708L8.707 8l5.147 5.146a.5.5 0 0 1-.708.708L8 8.707l-5.146 5.147a.5.5 0 0 1-.708-.708L7.293 8 2.146 2.854Z" />
      </svg>
    </span>
  </li>
</template>

<script setup>
import { inject } from "vue"

defineProps({
  tarea: Object,
  //required: true, //LO COMENTO SINO TIRA ERROR Y ADEMAS NO HACE FALTA NO ES COMO LOS PROPS DE ANTES
});

const tareas = inject("tareas"); 

const eliminar = (id) => {
  tareas.value = tareas.value.filter((el) => el.id !== id);// SI PONGO QUE SEA IGUAL BORRA TODO MENOS LA TAREA QUE YO CLIQUEO
};

const completado = (id) => {
  tareas.value = tareas.value.map((el) => {
    if (el.id === id) {
      el.estado = !el.estado;
    }
    return el; // MAP SIEMPRE RETORNA
  });
};
</script>

<style>

.form-control {
  margin: auto;
  width: 100%;
}

.tachado {
  text-decoration: line-through;
}

.list-group {
  margin-top: 1rem;
}

</style>