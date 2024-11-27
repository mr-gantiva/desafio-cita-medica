<script setup>
import { ref, computed } from 'vue';

const paciente = ref('');
const fecha = ref('');
const hora = ref('');
const gravedad = ref('');
const motivo = ref('');

const emit = defineEmits();

const isFormValid = computed(() => {
    return paciente.value && fecha.value && hora.value && gravedad.value && motivo.value;
});

const agregarCita = () => {
    const nuevaCita = {
        paciente: paciente.value,
        fecha: fecha.value,
        hora: hora.value,
        gravedad: gravedad.value,
        motivo: motivo.value,
    };

    // Emitir el evento con la nueva cita
    emit('agregarCita', nuevaCita);

    // Limpiar el formulario
    paciente.value = '';
    fecha.value = '';
    hora.value = '';
    gravedad.value = '';
    motivo.value = '';
};
</script>

<template>
    <div>
        <form @submit.prevent="agregarCita" class="formulario row g-3 p-5">
            <div class="col-auto">
                <label :style="{ color: paciente ? 'black' : 'red' }" class="form-label">Paciente</label>
                <input v-model="paciente" type="text" class="form-control" />
            </div>
            <div class="col-auto">
                <label :style="{ color: fecha ? 'black' : 'red' }" class="form-label">Fecha</label>
                <input v-model="fecha" type="date" class="form-control" />
            </div>
            <div class="col-auto">
                <label :style="{ color: hora ? 'black' : 'red' }" class="form-label">Hora</label>
                <input v-model="hora" type="time" class="form-control" />
            </div>
            <div class="col-auto">
                <label :style="{ color: gravedad ? 'black' : 'red' }" class="form-label">Gravedad</label>
                <select v-model="gravedad" class="form-select">
                    <option value="Baja">Baja</option>
                    <option value="Media">Media</option>
                    <option value="Alta">Alta</option>
                </select>
            </div>
            <div class="col-auto">
                <label :style="{ color: motivo ? 'black' : 'red' }" class="form-label">Motivo</label>
                <input v-model="motivo" type="text" class="form-control" />
            </div>

            <div class="d-grid gap-2 col-6 mx-auto">
                <button :disabled="!isFormValid" type="submit" class="btn btn-primary btn-lg">Agregar</button>
            </div>
        </form>
    </div>
</template>

<style scoped>
.formulario {
    background-color: #fff;
    border-radius: 20px;
    border: solid 1px #f0f0f0;
}

button:disabled {
    background-color: #ccc;
    cursor: not-allowed;
}

.btn-primary {
    background-color: #99CC00;
    border: none;
}
</style>