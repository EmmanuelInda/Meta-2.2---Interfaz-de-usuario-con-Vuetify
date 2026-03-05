<template>
  <v-table>
    <thead>
      <tr>
        <th class="text-left">Habilidad Técnica</th>
        <th class="text-left">Nivel de Dominio</th>
        <th class="text-left">Años de Experiencia</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="item in habilidades" :key="item.nombre">
        <td>{{ item.nombre }}</td>
        <td>{{ item.nivel }}</td>
        <td>{{ item.anios }}</td>
      </tr>
    </tbody>
  </v-table>
</template>

<script setup>
import { ref } from 'vue'

const habilidades = ref([
  { nombre: 'Vue.js 3', nivel: 'Intermedio', anios: 1 },
  { nombre: 'JavaScript (ES6+)', nivel: 'Avanzado', anios: 2 },
  { nombre: 'Vuetify 3', nivel: 'Básico', anios: 1 },
  { nombre: 'Git & GitHub', nivel: 'Intermedio', anios: 2 }
])
</script>
