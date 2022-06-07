<template>
  <div class="card mt-3">
    <div class="card-body d-flex justify-content-between aling-item-center">
      <span role="button" @click="filtrar('Activos')">Activos</span>
      <span role="button" @click="filtrar('Todos')">Todos</span>
      <span role="button" @click="filtrar('Completados')">Completados</span>
    </div>
  </div>
</template>

<script setup>
import { inject } from "vue";

const estado = inject("estado");

const filtrar = (e) => {
  estado.value = e;
};
</script>

<style>

</style>