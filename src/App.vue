<template>
  <div>
    <!-- Navbar -->
    <Navbar />

    <!-- Contenido dinámico de las rutas -->
    <router-view />
  </div>
</template>

<script>
import Navbar from "./components/Navbar.vue";

export default {
  components: {
    Navbar,
  },
};
</script>
