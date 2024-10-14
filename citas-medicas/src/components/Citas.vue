<template>
    <div :style="{ backgroundColor: colorGravedad, color: textColor }" class="card">
      <h3>{{ cita.Paciente }}</h3>
      <p>Fecha: {{ cita.Fecha }}</p>
      <p>Hora: {{ cita.Hora }}</p>
      <p>Motivo: {{ cita.Motivo }}</p>
      <button @click="$emit('eliminar-cita', cita)" class="delete-button">Eliminar</button>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      cita: Object
    },
    computed: {
      colorGravedad() {
        return this.cita.Gravedad === 'Alta' ? 'red' : this.cita.Gravedad === 'Media' ? 'yellow' : 'green'
      },
      textColor() {
        return this.cita.Gravedad === 'Media' ? 'black' : 'white'
      }
    }
  }
  </script>
  
  <style scoped>
  .card {
    padding: 20px;
    margin: 10px;
    border-radius: 8px;
    box-shadow: 0 0 15px rgba(0, 0, 0, 0.2);
    color: inherit;
    max-width: 300px;
  }
  
  h3 {
    margin: 0;
    padding-bottom: 10px;
  }
  
  p {
    margin: 5px 0;
  }
  
  .delete-button {
    padding: 8px 12px;
    background-color: white;
    color: black; 
    border: 2px solid black; 
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s, color 0.3s;
  }
  
  .delete-button:hover {
    background-color: black; 
    color: white;
  }
  </style>
  