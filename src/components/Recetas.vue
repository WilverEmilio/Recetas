<template>
  <div>
    <div class="columns">  <!-- Aqui se muestran los botones de agregar y volver -->
      <div class="column">
        <b-button type="is-primary" @click="agregarReceta()">
          <b-icon icon="plus"></b-icon>&nbsp;Agregar
        </b-button>
        <b-table :data="recetas"> <!-- Aqui se muestra la tabla de recetas -->
          <b-table-column
            field="nombre"
            label="Nombre"
            sortable
            searchable
            v-slot="props"
          >
            {{ props.row.nombre }}
          </b-table-column>
          <b-table-column
            field="descripcion"
            label="Descripción"
            searchable
            sortable
            v-slot="props"
          >
            {{ props.row.descripcion }}
          </b-table-column>
          <b-table-column
            field="porciones"
            label="Porciones"
            numeric
            sortable
            searchable
            v-slot="props"
          >
            {{ props.row.porciones }}
          </b-table-column>
          <b-table-column field="id" label="Opciones" v-slot="props">
            <b-field grouped>
              <p class="control">
                <b-button @click="editarReceta(props.row)" type="is-warning">
                  <b-icon icon="pencil"></b-icon>
                </b-button>
              </p>
              <p class="control">
                <b-button @click="eliminarReceta(props.row)" type="is-danger">
                  <b-icon icon="delete"></b-icon>
                </b-button>
              </p>
            </b-field>
          </b-table-column>
        </b-table>
      </div>
    </div>
  </div>
</template>
<script> // Importa el servicio de recetas
import RecetasService from "../services/RecetasService";
export default { // Exporta el componente
  data: () => ({
    recetas: [],
    cargando: false,
  }),
  async mounted() {
    await this.obtenerRecetas();
  },
  methods: { // Métodos del componente
    async obtenerRecetas() {
      this.cargando = true;
      this.recetas = await RecetasService.obtenerRecetas();
      this.cargando = false;
    },
    editarReceta(receta) { // Edita la receta
      this.$router.push({
        name: "EditarReceta",
        params: {
          id: receta.id,
        },
      });
    },
    async eliminarReceta(receta) { // Elimina la receta
      this.$buefy.dialog.confirm({ // Muestra un dialogo de confirmación
        title: "Eliminando receta",
        message: "¿Eliminar? esta opción no se puede deshacer",
        confirmText: "Sí, eliminar",
        cancelText: "No",
        type: "is-danger",
        hasIcon: true,
        onConfirm: async () => {
          await RecetasService.eliminarReceta(receta.id);
          await this.obtenerRecetas();
          this.$buefy.toast.open("Receta eliminada");
        },
      });
    },
    agregarReceta() { // Agrega una receta
      this.$router.push({
        name: "NuevaReceta",
      });
    },
  },
};
</script>
