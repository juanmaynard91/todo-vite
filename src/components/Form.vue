<template>
  <h1 class="title">{{ msg }}</h1>

  <form @submit.prevent="formulario">
    <input type="text" class="form-control" placeholder="agregar tareas.." v-model.trim="texto" />
  </form>
</template>

<script setup>
import { ref, inject } from "vue";
import Swal from "sweetalert2";

defineProps({
  msg: String,
});

const tareas = inject("tareas");
const texto = ref("");

const formulario = () => {
  if (texto.value === "") {
    Swal.fire({
      title: "Error!",
      text: "No se puede ingresar vacio",
      icon: "error",
    });
    return;
  } else {
    const tarea = {
      name: texto.value, // IMPORTANTE EL VALUE POQUE SINO NO SE QUE ESTOY INGRESANDO PA COMO QUERES QUE LO AGREGE AL ARRAY DE TAREAS
      estado: false,
      id: Date.now(),
    };
    tareas.value.push(tarea);
    texto.value = "";
    //console.log(tarea.estado);
  }
};

</script>

<style scoped>
.title {
  color: white;
  padding-top: 30px;
  text-transform: uppercase;
  margin-bottom: 1rem;
}
</style>
