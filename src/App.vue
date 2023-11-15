<template> <!-- Aqui el componente principal el cual muestra a simple vista todos los demás componentes -->
  <div id="app">
    <div class="main-bg">
  <div>
    <b-navbar class="oculto-impresion" style="background: linear-gradient(to right, #e75528, #ffba97);">
      <template #brand>
        <b-navbar-item tag="a" target="_blank" :href="logo"> <!-- Aqui se muestra el logo de la web -->
          <img :src="logo" style="min-height: 85px" />
        </b-navbar-item>
      </template>
      <template #start> <!-- Aqui se muestran los botones de navegación -->
        <b-navbar-item
          tag="router-link"
          :to="{ name: 'Recetario' }"
          @click="setActiveSection('Recetario')"
          :class="{ 'active-section': activeSection === 'Recetario' }"
        >
          <b-icon icon="chef-hat"></b-icon>&nbsp;Recetario
        </b-navbar-item>
        <b-navbar-item
          tag="router-link"
          :to="{ name: 'NuevaReceta' }"
          @click="setActiveSection('NuevaReceta')"
          :class="{ 'active-section': activeSection === 'NuevaReceta' }"
        >
          <b-icon icon="plus" class="mr-1"></b-icon>Nueva receta
        </b-navbar-item>
        <b-navbar-item
          tag="router-link"
          :to="{ name: 'Recetas' }"
          @click="setActiveSection('Recetas')"
          :class="{ 'active-section': activeSection === 'Recetas' }"
        >
          <b-icon icon="book-open-page-variant"></b-icon>&nbsp;Gestionar recetas
        </b-navbar-item>
        <b-navbar-item
          tag="router-link"
          :to="{ name: 'AcercaDe' }"
          @click="setActiveSection('AcercaDe')"
          :class="{ 'active-section': activeSection === 'AcercaDe' }"
        >
          <b-icon icon="information"></b-icon>&nbsp;Acerca de Nosotros
        </b-navbar-item>
      </template>
      <template #end>
        <b-navbar-item tag="div"></b-navbar-item>
      </template>
    </b-navbar>
    <section class="section sin-espacios-al-imprimir"> <!-- Aqui se muestran los componentes -->
      <transition name="fade" mode="out-in">
        <router-view />
      </transition>
      <div v-if="showPreloader" class="preloader">
        <img @load="onPreloaderLoad" src="./assets/img/preloader.gif" alt="Preloader" />
      </div>
    </section>
    <footer class="footer oculto-impresion" style="background-color: #f0f0f0; padding: 20px;">
      <div class="content has-text-centered">
        <div class="copyright">© Todos los derechos reservados 2023</div>
      </div>
    </footer>
  </div>
</div>
  </div>
</template>

<script src="js/bootstrap.min.js"></script>
<script> //-- Aqui se importan los componentes -->
import Logo from "@/assets/img/Whack-Dark.png";

export default {
  name: "app",
  data: () => ({
    logo: Logo,
    activeSection: null,
    showPreloader: false,
  }),
  methods: {
    setActiveSection(section) {
      this.activeSection = section;
      this.showPreloader = true;
    },
    onPreloaderLoad() {
      this.showPreloader = false; // Ocultar preloader después de la carga del gif
    },
  },
};
</script>

<style scoped>
/* Estilos específicos del componente */
@media print {
  .oculto-impresion,
  .oculto-impresion * {
    display: none !important;
  }
  .section.sin-espacios-al-imprimir {
    margin: 5px !important;
    padding: 7px !important;
  }
}
.preloader {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  background: rgba(255, 255, 255, 0.9); /* Fondo blanco semitransparente */
}
.main-bg {
  background-color: #f2f2f2;
  background-image: url('./assets/img/fondovegetales.jpg');
  background-size: cover;
  background-position: center;
  min-height: 100vh;
  background-blend-mode: overlay;
}

</style>
