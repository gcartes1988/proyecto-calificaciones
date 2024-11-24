<template>
  <div class="container mt-5">
    <form @submit.prevent="registrar">
      <div class="mb-3 text-center">
        <label for="nombre">Nombre:</label>
        <input v-model="registro.nombre" type="text" id="nombre" class="form-control" required />
      </div>
      <div class="mb-3 text-center">
        <label for="correo">Correo:</label>
        <input v-model="registro.correo" type="email" id="correo" class="form-control" required />
      </div>
      <div class="mb-3 text-center">
        <label for="contraseña">Contraseña:</label>
        <input
          v-model="registro.contraseña"
          type="password"
          id="contraseña"
          class="form-control"
        />
        <div v-if="errores.contraseña" class="text-danger">
          {{ errores.contraseña }}
        </div>
      </div>
      <div class="mb-3 text-center">
        <label for="repetirContraseña">Repetir Contraseña:</label>
        <input
          v-model="registro.repetirContraseña"
          type="password"
          id="repetirContraseña"
          class="form-control"
        />
        <div v-if="errores.repetirContraseña" class="text-danger">
          {{ errores.repetirContraseña }}
        </div>
      </div>
      <button class="btn btn-success w-100">Enviar</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      registro: {
        nombre: "",
        correo: "",
        contraseña: "",
        repetirContraseña: "",
      },
      errores: {
        contraseña: "",
        repetirContraseña: "",
      },
    };
  },
  methods: {
    registrar() {
      const { contraseña, repetirContraseña } = this.registro;

      // Reinicia los errores
      this.errores.contraseña = "";
      this.errores.repetirContraseña = "";

      // Validación de Contraseña
      if (!contraseña) {
        this.errores.contraseña = "El campo contraseña es requerido.";
      }

      // Validación de Repetir Contraseña
      if (!repetirContraseña) {
        this.errores.repetirContraseña = "El campo repetir contraseña es requerido.";
      } else if (contraseña !== repetirContraseña) {
        this.errores.repetirContraseña = "Las contraseñas no coinciden.";
      }

      // Si no hay errores, muestra un mensaje de éxito
      if (!this.errores.contraseña && !this.errores.repetirContraseña) {
        alert("El registro se ha realizado correctamente.");
      }
    },
  },
};
</script>
