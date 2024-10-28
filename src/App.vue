<template>
  <q-layout view="lHh Lpr lFf" class="bg-light-gray">
    <q-header elevated class="bg-gray-800 text-white">
      <q-toolbar class="toolbar">
        <q-img
          src="https://fb520d9d80.cbaul-cdnwnd.com/8d343d7d4cc8ddcd635e88b913853fd2/200000022-df47fdf481/sena-colombia-logo-green39a900.png?ph=fb520d9d80" 
          style="width: 50px; height: 50px;"
          class="q-mr-md" 
        />
        <q-toolbar-title class="font-title">Gestión de Actividades</q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-page-container class="bg-light-gray text-dark">
      <q-tabs
        v-model="currentTab"
        class="text-white bg-gray-800"
        align="justify"
        @update:model-value="navigateTo"
      >
        <q-tab name="actividades" label="Actividades" icon="list" />
        <q-tab name="agregar" label="Agregar Actividad" icon="add" />
      </q-tabs>

      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';

const router = useRouter();
const currentTab = ref('actividades');

function navigateTo(tab) {
  if (tab === 'actividades') {
    router.push('/');
  } else if (tab === 'agregar') {
    router.push('/agregar');
  } else if (tab === 'editar') {
    router.push('/editar');
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Pacifico&display=swap');

.q-tabs {
  border-bottom: 2px solid rgba(255, 255, 255, 0.5);
}

.bg-light-gray {
  background-color: #202020; 
}

.bg-gray-800 {
  background-color: #3a3a3a; 
}

.text-dark {
  color: #ffffff; 
}

.font-title {
  font-family: 'Pacifico', cursive; 
  font-size: 1.8em; 
}

.toolbar {
  height: 80px; 
  padding: 0 20px; 
  align-items: center; 
}
</style>
