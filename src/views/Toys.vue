<template>
  <div class="deep-purple accent-2">
    <toys-form
      :showForm="showForm"
      @close-form="showForm = false"
      @save-form="showForm = false"
    ></toys-form>
    <v-container>
      <v-row>
        <h1>Juguetes</h1>
        <v-spacer></v-spacer>
        <v-btn color="success" @click.prevent="showForm = true">Nuevo</v-btn>
      </v-row>
    </v-container>
    <v-container>
      <v-simple-table class="teal lighten-5">
        <thead>
          <tr>
            <th class="text-left">Código</th>
            <th class="text-left">Nombre</th>
            <th class="text-left">Stock</th>
            <th class="text-left">Precio</th>
            <th class="text-left"></th>
            <th class="text-left"></th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="toy in toys" :key="toy.id">
            <td>{{ toy.data.code }}</td>
            <td>{{ toy.data.name }}</td>
            <td>{{ toy.data.stock }}</td>
            <td>{{ toy.data.price }}</td>
            <td>
              <v-btn text color="warning" @click="modifyToy(toy)">editar</v-btn>
            </td>
            <td>
              <v-btn text color="danger" @click="removeToy(toy.id)"
                >eliminar</v-btn
              >
            </td>
          </tr>
        </tbody>
      </v-simple-table>
    </v-container>
  </div>
</template>

<script>
import ToysForm from "@/components/ToysForm";
import { mapState, mapActions } from "vuex";
export default {
  name: "Toy",
  components: {
    ToysForm,
  },
  data() {
    return {
      showForm: false,
    };
  },
  computed: {
    ...mapState(["toys"]),
  },
  methods: {
    ...mapActions(["getToys", "deleteToy", "editToy"]),
    removeToy(toyId) {
      if (confirm("¿Desea eliminar el producto seleccionado?")) {
        this.deleteToy(toyId);
      }
    },
    modifyToy(toy) {
      this.editToy(toy);
      this.showForm = true;
    },
  },
  created() {
    this.getToys();
  },
};
</script>

<style>
</style>