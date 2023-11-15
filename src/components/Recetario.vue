<template>
  <div>
    <div class="columns"> <!-- Aqui se muestra el formulario de busqueda -->
      <div class="column">
        <b-field label="Buscar receta"> <!-- Aqui se muestra el input de busqueda -->
          <b-input
            @keyup.native="buscar()"
            v-model="busqueda"
            placeholder="Ingresa el término de búsqueda"
            icon-right="close-circle"
            icon-right-clickable
            @icon-right-click="cancelarBusqueda()"
            :loading="cargando"
          ></b-input>
        </b-field>
      </div>
    </div>
    <div class="columns is-multiline is-desktop"> <!-- Aqui se muestran las tarjetas de recetas -->
      <div
        class="column is-one-third-desktop"
        v-for="(receta, i) in recetas"
        :key="i"
      >
        <tarjeta-receta :receta="receta"></tarjeta-receta>
      </div>
    </div>
  </div>
</template>
<script> //-- Aqui se importan los servicios y componentes -->
import RecetasService from "../services/RecetasService";
import TarjetaReceta from "./TarjetaReceta.vue";
import Utiles from "../services/Utiles";
export default { //-- Aqui se exporta el componente -->
  components: { TarjetaReceta },
  data: () => ({
    recetas: [],
    cargando: false,
    busqueda: "",
  }),
  async mounted() { //-- Aqui se obtienen las recetas -->
    await this.obtenerRecetas();
    this.buscar = Utiles.debounce(async () => {
      if (!this.busqueda) {
        await this.cancelarBusqueda();
        return;
      }
      this.cargando = true; //-- Aqui se busca la receta -->
      this.recetas = await RecetasService.buscarRecetas(this.busqueda);
      this.cargando = false;
    }, 500);
  },
  methods: { //-- Aqui se cancela la busqueda -->
    async cancelarBusqueda() {
      if (!this.busqueda) return;
      this.busqueda = "";
      await this.obtenerRecetas();
    },
    async obtenerRecetas() { //-- Aqui se obtienen las recetas -->
      this.cargando = true;
      this.recetas = await RecetasService.obtenerRecetas();
      this.cargando = false;
    },
  },
};
</script>
<style scoped>

</style>
