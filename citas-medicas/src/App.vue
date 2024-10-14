<template>
  <div id="app" class="app-container">
    <h1>Administrador de Citas Médicas</h1>
    <Formulario @nueva-cita="agregarCita"/>
    <p v-if="citas.length === 0">Aún no hay consultas registradas</p>
    <Citas v-for="(cita, index) in citas" :key="index" :cita="cita" @eliminar-cita="eliminarCita"/>
  </div>
</template>

<script>
import Formulario from './components/Formulario.vue'
import Citas from './components/Citas.vue'

export default {
  components: {
    Formulario,
    Citas
  },
  data() {
    return {
      citas: []
    }
  },
  methods: {
    agregarCita(cita) {
      this.citas.push(cita)
    },
    eliminarCita(citaAEliminar) {
      this.citas = this.citas.filter(cita => cita !== citaAEliminar)
    }
  }
}
</script>

<style>
.app-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
  background-color: #ffffff; 
  height: 100vh;
}

h1 {
  color: #333;
  margin-bottom: 20px;
}

form {
  margin-bottom: 20px;
}
</style>
