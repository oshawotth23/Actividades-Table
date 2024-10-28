<template>
  <div class="q-pa-sm">
    <q-card flat bordered class="activity-card">
      <q-card-section>
        <h2 class="title">Lista de Actividades</h2>
      </q-card-section>
      <q-card-section>
        <q-table :rows="activities" :columns="columns" row-key="id" flat bordered class="q-my-sm">
          <template v-slot:body-cell-actions="props">
            <q-td :props="props" class="actions-cell">
              <q-btn dense color="green-7" icon="edit" @click="editActivity(props.row)" flat />
              <q-btn dense color="red" icon="delete" @click="deleteActivity(props.row.id)" flat />
            </q-td>
          </template>

          <template v-slot:body-cell-status="props">
            <q-td :props="props">
              <span :class="getStatusClass(props.row.status)">
                {{ props.row.status }}
              </span>
            </q-td>
          </template>
        </q-table>
      </q-card-section>
    </q-card>
  </div>
</template>

<script setup>
import { useAdminStore } from '../stores/admin.js';
import { useRouter } from 'vue-router';
import { computed } from 'vue';

const store = useAdminStore();
const router = useRouter();

const activities = computed(() => store.activities);
const columns = [
  { name: 'description', label: 'Descripción', field: 'description', align: 'left' },
  { name: 'date', label: 'Fecha', field: 'date', align: 'center' },
  { name: 'status', label: 'Estado', field: 'status', align: 'center' },
  { name: 'actions', label: 'Acciones', field: 'actions', align: 'center' }
];

function editActivity(activity) {
  store.setSelectedActivity(activity);
  router.push('/editar');
}

function deleteActivity(activityId) {
  store.deleteActivity(activityId);
}

function getStatusClass(status) {
  return status === 'Completado' ? 'completado' : 'pendiente';
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Pacifico&display=swap');

.activity-card {
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  padding: 8px;
  background-color: #ffffff; 
  border: 1px solid #ccc; 
}

.title {
  margin: 0;
  padding: 8px;
  text-align: center;
  color: #3a3a3a; 
  font-size: 1.5rem;
  font-family: 'Fredoka One';
}

.actions-cell {
  display: flex;
  justify-content: center;
  gap: 6px;
}

.completado {
  color: #388e3c; 
  font-weight: bold;
}

.pendiente {
  color: #d32f2f;
  font-weight: bold;
}

.q-table {
  background-color: #a2e0f3;
}

.q-table th {
  background-color: #3a3a3a;
  color: white;
  font-weight: bold;
}

.q-table td {
  color: #333;
}

.hover\:bg-gray-300:hover {
  background-color: #d1d1d1; 
}
</style>
