<template>
    <form @submit.prevent="agregarCita" class="form-horizontal">
      <div v-for="(label, index) in campos" :key="index" class="form-group">
        <label :style="{ color: valores[label] ? 'black' : 'red' }">{{ label }}</label>
        <div v-if="label === 'Gravedad'">
          <select v-model="valores[label]">
            <option value="" disabled selected>Indique Gravedad</option>
            <option value="Baja">Baja</option>
            <option value="Media">Media</option>
            <option value="Alta">Alta</option>
          </select>
        </div>
        <div v-else>
          <input v-model="valores[label]" :type="getType(label)" :placeholder="label"/>
        </div>
      </div>
      <button :disabled="!formularioCompleto">Agregar</button>
    </form>
  </template>
  
  <script>
  export default {
    data() {
      return {
        valores: {
          Paciente: '',
          Fecha: '',
          Hora: '',
          Gravedad: '',
          Motivo: ''
        }
      }
    },
    computed: {
      formularioCompleto() {
        return Object.values(this.valores).every(valor => valor)
      }
    },
    methods: {
      agregarCita() {
        this.$emit('nueva-cita', { ...this.valores });
        this.valores = {
          Paciente: '',
          Fecha: '',
          Hora: '',
          Gravedad: '',
          Motivo: ''
        }
      },
      getType(label) {
        switch (label) {
          case 'Fecha':
            return 'date'
          case 'Hora':
            return 'time'
          default:
            return 'text'
        }
      }
    },
    props: {
      campos: {
        type: Array,
        default: () => ['Paciente', 'Fecha', 'Hora', 'Gravedad', 'Motivo']
      }
    }
  }
  </script>
  
  <style scoped>
  form {
    display: flex;
    align-items: center;
  }
  
  .form-group {
    display: flex;
    flex-direction: column;
    margin-right: 15px;
  }
  
  label {
    display: block;
    margin-bottom: 5px;
  }
  
  input, select {
    padding: 8px;
    border: 1px solid #ccc;
    border-radius: 4px;
  }
  
  button {
    padding: 10px;
    background-color: blue;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  
  button:disabled {
    background-color: grey;
    cursor: not-allowed;
  }
  </style>
  