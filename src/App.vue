<script setup>
import { ref } from 'vue';
import FormularioCita from './components/FormularioCita.vue';
import CitaCard from './components/CitaCard.vue';

const citas = ref([]);

// Función para agregar una cita al arreglo
const agregarCita = (cita) => {
  citas.value.push(cita);
};

// Función para eliminar una cita del arreglo
const eliminarCita = (cita) => {
  citas.value = citas.value.filter((item) => item !== cita);
};
</script>

<template>

  <section class="container-fluid">
    <div class="container">
      <h1 class="py-5 text-center">Registro de Citas Médicas</h1>
      <FormularioCita @agregarCita="agregarCita" />

      <div v-if="citas.length === 0">
        <p class="text-center texto-rojo">Aún no hay consultas registradas.</p>
      </div>

      <div v-else class="row d-flex">
        <div v-for="(cita, index) in citas" :key="index" class="col-4">
          <CitaCard :cita="cita" @eliminarCita="eliminarCita(cita)" />
        </div>
      </div>
    </div>
  </section>
</template>

<style>
h1 {
  color: #009999;
}

.texto-rojo {
  color: red;
}
</style>
