<template>
  <div class="receta-container">
    <div class="receta-border"></div>
  <div class="card">
    <a @click="verDetalle()" class= "card-image">
      <foto-de-receta :receta="receta"></foto-de-receta></a>
    <div class="card-content">
      <div class="media">
        <div class="media-content">
          <p class="title is-4">{{ receta.nombre }}</p>
        </div>
      </div>
      <div class="content">
        {{ receta.descripcion }}
      </div>
    </div>
    <footer class="card-footer">
      <a @click="verDetalle()" class="card-footer-item">Ver&nbsp; <b-icon icon="book-open-outline"></b-icon></a>
    </footer>
  </div>
</div>
</template>
<script>
import FotoDeReceta from "./FotoDeReceta.vue";
export default {
  props: ["receta"],
  components: { FotoDeReceta },
  methods: {
    verDetalle() {
      this.$router.push({
        name: "DetalleReceta",
        params: {
          id: this.receta.id,
        },
      });
    },
  },
};
</script>
<style>
.tarjeta-receta {
  margin: 10px; /* Ajusta el valor según sea necesario */
}
.receta-container {
  position: relative;
}

.receta-border {
  position: absolute;
  top: -10px;
  left: -5px;
  right: -5px;
  bottom: -10px;
  box-sizing: border-box;
  padding: 10px;
  background: linear-gradient(to bottom, rgb(255, 145, 0), #f7dfb1);
}
</style>
