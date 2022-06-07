<template>
  <div class="container">
    <Form msg="Lista de Tareas" />
    <Lista />
  </div>
</template>


<script setup>
import { provide, ref, watchEffect } from "vue";
import Form from "./components/Form.vue";
import Lista from "./components/Lista.vue";

const tareas = ref([]);
provide("tareas", tareas); // provide: paso algo reactivo a otros componentes como un props

if (localStorage.getItem("tareas")) {
  // si existe lo parseo a array(en este caso ya que taras es un array)
  tareas.value = JSON.parse(localStorage.getItem("tareas"));
}

watchEffect(() => {
  // para vigilar lo reactivo y usar el localstorage hay que usar watcheffect
  localStorage.setItem("tareas", JSON.stringify(tareas.value)); // primero lo creo y lo guardo como string
});
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Anton&family=Bebas+Neue&family=Roboto:wght@300&display=swap");

* {
  margin: 0;
  padding: 0;
}

#app {
  height: 100vh;
  font-family: "Anton", sans-serif;
  font-family: "Bebas Neue", cursive;
  font-family: "Roboto", sans-serif;
  text-align: center;
  background: linear-gradient(to right, #00416a, #799f0c);
  background-size: 200% 200%; /* para que ande la animacion tengo que agregarle el tamaña a la app */
  animation: bg-animado 5s linear infinite alternate;
}

@keyframes bg-animado {
  from {
    background-position: 0, 0;
  }
  to {
    background-position: 100% 100%;
  }
}

@media (max-width: 375px) {
  #app {
    height: 160vh;
  }
}
</style>
