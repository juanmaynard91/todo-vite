<template>
  <h1 class="title">{{ msg }}</h1>

  <form @submit.prevent="formulario">
    <input
      type="text"
      class="form-control"
      placeholder="agregar tareas.."
      v-model.trim="texto"
    />
  </form>

  <!--<ul class="list-group">
    <Items
      v-for="tarea in tareas"
      :key="tarea.id"
      :tarea="tarea"
      @emitEliminado="eliminarTarea(tarea.id)"
      @emitCompletado="tareaRealizada(tarea.id)"
      :class="{ tachado: tarea.estado }"
    />

    <li class="form-control" v-if="tareas.length === 0">No hay tareas</li>
    <Footer v-else />

    <Filtro />
  </ul>-->
</template>

<script setup>
//import Items from "../components/Items.vue";
//import Footer from "./Footer.vue";
//import Filtro from "./Filtro.vue";
import { ref, inject } from "vue";
import Swal from "sweetalert2";

defineProps({
  msg: String,
});

const tareas = inject("tareas");
const texto = ref("");
//const estado = ref("Todos"); //por defecto muestro todas las tareas

const formulario = () => {
  if (texto.value === "") {
    //alert("No se puede ingresar vacio");
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

/*const eliminarTarea = (id) => {
  tareas.value = tareas.value.filter((el) => el.id !== id); // SI PONGO QUE SEA IGUAL BORRA TODO MENOS LA TAREA QUE YO CLIQUEO
};

const tareaRealizada = (id) => {
  tareas.value = tareas.value.map((el) => {
    if (el.id === id) {
      el.estado = !el.estado;
    }
    return el; // RETURN YA QUE ESTOY MOSTRANDO SIEMPRE EN QUE ESTADO SE ENCUENTRA (PARA QUE SE VEA TACHADO O NO)
  });
};

const tareas = computed(() => { //COMPUTED AL V-FOR 
  if (estado.value === "Todos") {
    return todasLasTareas.value;
  }
  if (estado.value === "Activos") {
    return todasLasTareas.value.filter((el) => el.estado === false);
  }
  if (estado.value === "Completados") {
    return todasLasTareas.value.filter((el) => el.estado === true);
  }
});

provide("estado", estado);*/
</script>

<style scoped>
.title {
  color: white;
  padding-top: 12px;
  text-transform: uppercase;
  margin-bottom: 1rem;
}
</style>
