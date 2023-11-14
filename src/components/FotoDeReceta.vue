<template>
  <img
  :src="fotoDeReceta()"
  :alt="'Foto de ' + receta.nombre"
  class="recipe-image"
>
</template>
<script>
import RecetasService from "../services/RecetasService"
export default {
  props: ["receta"],
  methods: {
    fotoDeReceta() {
      if (!this.receta.foto) {
        return false;
      }
      return RecetasService.ubicacionFoto(this.receta.foto);
    },
  },
};
</script>
<style scoped>
.recipe-image {
  transition: transform 0.2s;
}

.recipe-image:hover {
  transform: scale(1.1);
  box-shadow: 0 0 10px rgba(0,0,0,0.3);
}
</style>
