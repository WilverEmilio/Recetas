<template> <!-- Aqui se muestra el detalle de la receta -->
  <div class="columns">
    <div class="column" style="padding: 0; margin: 0"> <!-- Aqui se muestra el detalle de la receta -->
      <div class="columns">
        <div class="column is-one-third">
          <foto-de-receta :receta="receta"></foto-de-receta>
        </div>
        <div class="column">
          <div class="media">
            <div class="media-content">
              <p class="title is-size-2">{{ receta.nombre }}</p>
            </div>
          </div>
          <div class="content is-medium">
            <p class="is-size-6">{{ receta.descripcion }}</p>
            <strong>Porciones&nbsp;</strong> {{ porciones }}
            <b-field
              class="oculto-impresion"
              grouped
              label="Porciones"
              message="Usted puede cambiar las porciones. La cantidad de ingredientes se ajustará"
            >
              <b-numberinput v-model="porciones"></b-numberinput>
            </b-field>
            <b-field>
              <b-button
                :loading="imprimiendo"
                class="oculto-impresion"
                @click="imprimir()"
                type="is-success is-light"
              >
                <b-icon icon="printer"></b-icon>&nbsp; Imprimir</b-button
              >
            </b-field>
          </div>
        </div>
      </div>

      <div class="content">
        <div class="columns">
          <div class="column">
            <h2 class="has-text-centered is-2">Ingredientes</h2>
            <b-field
              v-for="(ingrediente, indiceIngrediente) in receta.ingredientes"
              :key="indiceIngrediente"
            >
              <b-checkbox>{{ nombreIngrediente(ingrediente) }}</b-checkbox>
            </b-field>
          </div>
          <div class="column">
            <h2 class="has-text-centered is-2">Preparación</h2>
            <div v-for="(paso, indicePaso) in receta.pasos" :key="indicePaso">
              <b-checkbox class="mb-2">
                <strong>Paso {{ indicePaso + 1 }}</strong>
                <p>{{ paso }}</p>
              </b-checkbox>
            </div>
          </div>
        </div>
        <div class="columns" v-show="imprimiendo">
          <div class="column">
            <div class="print-footer">
              <p>
                <b-icon icon="copyright"></b-icon>
                <strong>WHACK RECETAS </strong
                >¡Gracias por usar nuestra web!
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script> //-- Aqui se importan los componentes -->
import Constantes from "../Constantes"; // Aqui se importan los componentes
import RecetasService from "../services/RecetasService"; // Importa el servicio de recetas
import FotoDeReceta from "./FotoDeReceta.vue"; // Importa el componente FotoDeReceta
export default { // Exporta el componente
  components: { FotoDeReceta }, // Componentes del componente
  data: () => ({ // Datos del componente
    receta: {},
    porciones: null,
    imprimiendo: false,
  }),
  methods: { // Métodos del componente
    async imprimir() { // Imprime la receta
      this.imprimiendo = true; // Muestra el footer de impresión
      const tituloOriginal = document.title; // Guarda el titulo original
      document.title = "Receta de " + this.receta.nombre; // Cambia el titulo
      await this.$nextTick(); // Espera a que se actualice el DOM
      window.print(); // Imprime la receta
      document.title = tituloOriginal; // Restaura el titulo original
      this.imprimiendo = false; // Oculta el footer de impresión
    },
    nombreIngrediente(ingrediente) { // Devuelve el nombre del ingrediente
      if (ingrediente.unidadMedida === Constantes.AL_GUSTO) { // Si es al gusto devuelve el nombre del ingrediente y al gusto
        return `${ingrediente.nombre} ${Constantes.AL_GUSTO}`;
      } else {
        const cantidad = this.cantidadIngrediente(ingrediente.cantidad); // Devuelve la cantidad del ingrediente
        return `${cantidad} ${ingrediente.unidadMedida}(s) de ${ingrediente.nombre}`;
      }
    },
    cantidadIngrediente(cantidad) {
      return ((cantidad * this.porciones) / this.receta.porciones).toFixed(1);
    },
  },
  async mounted() { // Cuando se monta el componente
    const idReceta = this.$route.params.id;  // Obtiene el id de la receta
    const receta = await RecetasService.obtenerRecetaPorId(idReceta); // Obtiene la receta por id
    // Arregla los pasos porque los regresa como objetos
    receta.pasos = receta.pasos.map((objetoPaso) => objetoPaso.paso);
    this.receta = receta; // Asigna la receta
    this.porciones = this.receta.porciones; // Asigna las porciones
  },
};
</script>
<style >
@media print {
  .print-footer {
    position: fixed;
    bottom: 0;
    left: 0;
    width: 100%;
    text-align: center;
  }
}
</style>
