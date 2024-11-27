<script setup>
import { defineProps, defineEmits, computed } from 'vue';

const props = defineProps({
    cita: {
        type: Object,
        required: true,
    },
});

const emit = defineEmits(['eliminarCita']);

const fondoGravedad = computed(() => {
    switch (props.cita.gravedad) {
        case 'Baja':
            return 'green';
        case 'Media':
            return 'yellow';
        case 'Alta':
            return 'red';
        default:
            return 'white';
    }
});

const eliminarCita = () => {
    emit('eliminarCita', props.cita);
};

</script>

<!-- src/components/CitaCard.vue -->
<template>
    <div :style="{ border: `2px solid ${fondoGravedad}` }" class="cita-card" data-aos="fade-up">
        <div class="d-flex justify-content-between">
            <p><strong>Nombre:</strong> {{ cita.paciente }}</p>
            <div class="gravedad__color" :style="{ backgroundColor: fondoGravedad }"></div>
        </div>
        <p><strong>Fecha:</strong> {{ cita.fecha }} <strong>Hora:</strong> {{ cita.hora }}</p>
        <p><strong>Motivo:</strong> {{ cita.motivo }}</p>
        <p><strong>Gravedad:</strong> {{ cita.gravedad }}</p>
        <button @click="eliminarCita" class="btn btn-danger">Eliminar</button>
    </div>
</template>

<style scoped>
.cita-card {
    padding: 15px;
    margin: 10px;
    border-radius: 8px;
    color: white;
    background-color: white;
}

.cita-card h3 {
    color: #049C9A;
}

.cita-card p {
    color: #747473;
}

button {
    margin-top: 10px;
    padding: 5px 10px;
    background-color: #fff;
    color: black;
    border: 2px solid red;
    cursor: pointer;
}

.gravedad__color {
    width: 20px;
    height: 20px;
    border-radius: 50%;
}
</style>