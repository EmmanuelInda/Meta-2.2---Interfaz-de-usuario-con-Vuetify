<template>
  <v-card class="mx-auto" max-width="400">
    <v-img :src="url" height="200px" cover></v-img>
    <v-card-title>{{ titulo }}</v-card-title>
    <v-card-subtitle>Autor: {{ autor }}</v-card-subtitle>
    <v-card-text>{{ descripcion }}</v-card-text>
  </v-card>
</template>

<script setup>
defineProps({
  url: {
    type: String,
    required: true
  },
  titulo: {
    type: String,
    required: true
  },
  descripcion: {
    type: String,
    required: true
  },
  autor: {
    type: String,
    required: true
  }
})
</script>
