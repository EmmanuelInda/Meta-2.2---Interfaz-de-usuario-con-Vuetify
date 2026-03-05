<template>
  <v-app>
    <AppHeader />
    
    <v-main>
      <v-container>
        <v-alert
          v-if="error"
          type="error"
          class="mb-4"
          closable
          @click:close="error = null"
        >
          {{ error }}
        </v-alert>

        <v-row class="mb-6">
          <v-col cols="12" md="6">
            <TarjetaConImagen
              v-if="tarjeta1.url"
              :url="tarjeta1.url"
              :titulo="tarjeta1.titulo"
              :descripcion="tarjeta1.descripcion"
              :autor="tarjeta1.autor"
            />
          </v-col>
          <v-col cols="12" md="6">
            <TarjetaConImagen
              v-if="tarjeta2.url"
              :url="tarjeta2.url"
              :titulo="tarjeta2.titulo"
              :descripcion="tarjeta2.descripcion"
              :autor="tarjeta2.autor"
            />
          </v-col>
        </v-row>

        <div class="text-center mb-6">
          <v-btn
            color="secondary"
            size="x-large"
            :loading="cargando"
            :disabled="cargando"
            @click="actualizarImagenes"
          >
            Obtener Nuevas Imágenes
          </v-btn>
        </div>

        <v-row>
          <v-col cols="12">
            <TablaDeDatos />
          </v-col>
        </v-row>
      </v-container>
    </v-main>

    <AppFooter />
  </v-app>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import AppHeader from './components/AppHeader.vue'
import AppFooter from './components/AppFooter.vue'
import TarjetaConImagen from './components/TarjetaConImagen.vue'
import TablaDeDatos from './components/TablaDeDatos.vue'

const cargando = ref(false)
const error = ref(null)

const tarjeta1 = ref({
  url: '',
  titulo: 'Fotografía Aleatoria 1',
  descripcion: 'Descripción obtenida para la primera tarjeta de presentación.',
  autor: ''
})

const tarjeta2 = ref({
  url: '',
  titulo: 'Fotografía Aleatoria 2',
  descripcion: 'Descripción obtenida para la segunda tarjeta de presentación.',
  autor: ''
})

const obtenerIndicesAleatorios = (max) => {
  const idx1 = Math.floor(Math.random() * max)
  let idx2 = Math.floor(Math.random() * max)
  
  while (idx1 === idx2) {
    idx2 = Math.floor(Math.random() * max)
  }
  
  return [idx1, idx2]
}

const actualizarImagenes = async () => {
  cargando.value = true
  error.value = null

  try {
    const respuesta = await fetch('https://picsum.photos/v2/list?page=1&limit=50')
    
    if (!respuesta.ok) {
      throw new Error('Error de red al obtener la lista de imágenes')
    }
    
    const datos = await respuesta.json()
    
    if (!datos || datos.length < 2) {
      throw new Error('Formato de datos incorrecto')
    }

    const [idx1, idx2] = obtenerIndicesAleatorios(datos.length)
    const img1 = datos[idx1]
    const img2 = datos[idx2]

    tarjeta1.value.url = `https://picsum.photos/id/${img1.id}/300/200`
    tarjeta1.value.autor = img1.author

    tarjeta2.value.url = `https://picsum.photos/id/${img2.id}/300/200`
    tarjeta2.value.autor = img2.author

  } catch (e) {
    error.value = e.message || 'Error al conectar con la API de Picsum'
  } finally {
    cargando.value = false
  }
}

onMounted(() => {
  actualizarImagenes()
})
</script>
