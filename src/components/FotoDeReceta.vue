<template> <!-- Aqui se muestra la foto de la receta -->
  <img
  :src="fotoDeReceta()"
  :alt="'Foto de ' + receta.nombre"
  class="recipe-image"
>
</template>
<script>
import RecetasService from "../services/RecetasService" // Importa el servicio de recetas
export default { // Exporta el componente
  props: ["receta"],
  methods: { // Métodos del componente
    fotoDeReceta() { // Devuelve la foto de la receta
      if (!this.receta.foto) { // Si no hay foto devuelve falso
        return false;
      }
      return RecetasService.ubicacionFoto(this.receta.foto); // Devuelve la ubicación de la foto
    },
  },
};
</script>
<style scoped> /* Estilos específicos del componente */
.recipe-image {
  overflow: hidden;
  transition: all 0.2s;
}

.recipe-image:hover {
  overflow: hidden;
  transform: scale(1.05);
}
</style>
