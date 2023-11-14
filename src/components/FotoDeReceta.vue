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
  overflow: hidden;
  transition: all 0.2s;
}

.recipe-image:hover {
  overflow: hidden;
  transform: scale(1.05);
}
</style>
