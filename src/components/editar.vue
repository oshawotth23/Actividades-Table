<template>
  <div class="q-pa-md">
    <q-card flat bordered class="activity-card">
      <q-card-section>
        <h2 class="title">Editar Actividad</h2>
      </q-card-section>

      <q-form @submit="onSubmit" class="form-container">
        <q-input filled v-model="activity.description" label="Descripción" lazy-rules class="input-field" />
        <q-input filled v-model="activity.date" label="Fecha" type="date" lazy-rules class="input-field" />
        <q-select filled v-model="activity.status" :options="statusOptions" label="Estado" class="input-field" />
        <div class="button-container">
          <q-btn label="Guardar Cambios" color="primary" type="submit" />
        </div>
      </q-form>
    </q-card>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useAdminStore } from '../stores/admin.js';
import { Notify } from 'quasar';
import { useRouter } from 'vue-router';

const store = useAdminStore();
const router = useRouter();
const activity = ref({ description: '', date: '', status: '' });
const statusOptions = ['Completado', 'Pendiente'];

onMounted(() => {
  const selected = store.selectedActivity;
  if (selected) {
    activity.value = { ...selected };
  }
});

function onSubmit() {
  store.updateActivity(activity.value);
  Notify.create({ message: 'Actividad actualizada exitosamente', color: 'green' });
  setTimeout(() => {
    router.push('/');
  }, 500);
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
