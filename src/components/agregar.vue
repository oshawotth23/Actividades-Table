<template>
  <q-page class="q-pa-md">
    <q-card flat bordered class="activity-card">
      <q-card-section>
        <h2 class="title">Agregar Nueva Actividad</h2>
      </q-card-section>

      <q-form @submit="onSubmit" class="form-container">
        <q-input filled v-model="activityData.description" label="Descripción" lazy-rules class="input-field" />
        <q-input filled v-model="activityData.date" label="Fecha" type="date" lazy-rules class="input-field" />
        <q-select filled v-model="activityData.status" :options="statusOptions" label="Estado" class="input-field" />
        <div class="button-container">
          <q-btn label="Agregar" color="primary" type="submit" class="submit-btn" />
        </div>
      </q-form>
    </q-card>
  </q-page>
</template>

<script setup>
import { ref } from 'vue';
import { useAdminStore } from '../stores/admin.js';
import { Notify } from 'quasar';

const adminStore = useAdminStore();
const activityData = ref({ description: '', date: '', status: '' });
const statusOptions = ['Completado', 'Pendiente'];

function onSubmit() {
  if (!activityData.value.description) {
    Notify.create({ message: 'Por favor completa la descripción', color: 'red' });
    return;
  }
  if (!activityData.value.date) {
    Notify.create({ message: 'Por favor completa la fecha', color: 'red' });
    return;
  }
  if (!activityData.value.status) {
    Notify.create({ message: 'Por favor selecciona el estado', color: 'red' });
    return;
  }
  
  adminStore.addActivity({ ...activityData.value });
  activityData.value = { description: '', date: '', status: '' };
  Notify.create({ message: 'Actividad agregada exitosamente', color: 'green' });
}

</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Pacifico&display=swap');

.activity-card {
  width: 900px; 
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  padding: 20px;
  background-color: #ffffff;
  border: 1px solid #ccc;
  margin: 0 auto; 
}

.title {
  margin: 20px 0;
  text-align: center;
  color: #3a3a3a;
  font-size: 1.8rem;
  font-family: 'Pacifico', cursive; 
}

.form-container {
  padding: 10px; 
}

.input-field {
  margin-bottom: 20px;
}

.button-container {
  display: flex;
  justify-content: flex-end;
  margin-top: 20px;
}

.q-btn {
  padding: 10px 20px;
  font-weight: bold;
  background-color: #007bff;
  color: white;
}

.q-btn:hover {
  background-color: #0056b3;
}
</style>
