<template>
  <v-footer color="primary" app>
    <v-container>
      <v-row>
        <v-col cols="12" md="4" class="text-center text-md-left">
          <span>Jesús Emmanuel Inda Campos</span>
        </v-col>
        <v-col cols="12" md="4" class="text-center">
          <span>Matrícula: 1190328</span>
        </v-col>
        <v-col cols="12" md="4" class="text-center text-md-right">
          <span>&copy; {{ currentYear }} - jesus.inda13@uabc.edu.mx</span>
        </v-col>
      </v-row>
    </v-container>
  </v-footer>
</template>

<script setup>
import { ref } from 'vue'

const currentYear = ref(new Date().getFullYear())
</script>
