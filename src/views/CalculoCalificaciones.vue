<template>
    <div class="container mt-5">
      <form @submit.prevent="calcularPromedio">
        <div class="mb-3 text-center">
          <label for="nota1">Nota 1</label>
          <input v-model.number="notas.nota1" type="number" id="nota1" class="form-control" min="10" max="70" required />
        </div>
        <div class="mb-3 text-center">
          <label for="nota2">Nota 2</label>
          <input v-model.number="notas.nota2" type="number" id="nota2" class="form-control" min="10" max="70" required />
        </div>
        <div class="mb-3 text-center">
          <label for="nota3">Nota 3</label>
          <input v-model.number="notas.nota3" type="number" id="nota3" class="form-control" min="10" max="70" required />
        </div>
        <div class="mb-3 text-center">
          <label for="asistencia">Asistencia %</label>
          <input v-model.number="asistencia" type="number" id="asistencia" class="form-control" min="0" max="100" required />
        </div>
        <button class="btn btn-primary w-100">Calcular</button>
      </form>
      <div v-if="resultado.mensaje" class="mt-3 alert" :class="resultado.clase">
        {{ resultado.mensaje }}
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        notas: { nota1: 0, nota2: 0, nota3: 0 },
        asistencia: 0,
        resultado: { mensaje: "", clase: "" },
      };
    },
    methods: {
      calcularPromedio() {
        const { nota1, nota2, nota3 } = this.notas;
        if ([nota1, nota2, nota3].some((n) => n < 10 || n > 70) || this.asistencia < 0 || this.asistencia > 100) {
          this.resultado = {
            mensaje: "Por favor, ingrese valores válidos para las notas y la asistencia.",
            clase: "alert-danger",
          };
          return;
        }
        const promedio = nota1 * 0.35 + nota2 * 0.35 + nota3 * 0.3;
        this.resultado = {
          mensaje: `El promedio es: ${promedio.toFixed(2)}. Tu estado es: ${
            promedio >= 40 && this.asistencia >= 80 ? "Aprobado" : "Reprobado"
          }`,
          clase: promedio >= 40 && this.asistencia >= 80 ? "alert-success" : "alert-danger",
        };
      },
    },
  };
  </script>
  