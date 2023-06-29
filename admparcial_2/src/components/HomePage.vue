<template>
  <div class="fondo">
    <h1>Obras</h1>

    <v-col class="d-flex" cols="6" md="3" sm="3">
      <h2>Filtro</h2>
      <v-select
        v-model="selectedItems"
        :items="listarCategoria"
        solo

      ></v-select>
    </v-col>

    <v-card
      class="mx-auto card-desc"
      max-width="60%"
      v-if="selectedItems != 'Catálogo'"
    >
      <v-card-title class="titulo titulo-desc">{{
        selectedItems
      }}</v-card-title>
      <v-expand-transition>
        <div>
          <v-card-text>
            <p class="parr-desc">{{ descCategoria() }}</p>
          </v-card-text>
        </div>
      </v-expand-transition>
    </v-card>

    <v-item-group>
      <v-container>
        <v-row>
          <v-col
            v-for="obra in listarCatalogo"
            :key="obra.nombre"
            cols="12"
            md="4"
          >
            <v-item>
              <CardObra :obra="obra"></CardObra>
            </v-item>
          </v-col>
        </v-row>
      </v-container>
    </v-item-group>
    <FooterPage></FooterPage>
  </div>
</template>

<script>
import FooterPage from "@/components/FooterPage.vue";
import CardObra from "@/components/CardObra.vue";

export default {
  name: "HomePage",
  components: {
    FooterPage,
    CardObra,
  },
  data: () => ({
    selectedItems: "Catálogo",
    categorias: [],
    catalogoObras: [],
    catalogoFiltrado: [],    
  }),
  props: {
    msg: String,
  },
  computed: {
    listarCategoria() {
      var listCategoria = ["Catálogo"];
      for (let i = 0; i < this.categorias.length; i++) {
        listCategoria.push(this.categorias[i].titulo);
      }
      return listCategoria;
    },
    listarCatalogo() {
      var catalogoFiltrado = [];
      if (this.selectedItems == "Catálogo") {
        catalogoFiltrado = this.catalogoObras;
      } else {
        for (let i = 0; i < this.catalogoObras.length; i++) {
          if (this.catalogoObras[i].categoria == this.selectedItems)
            catalogoFiltrado.push(this.catalogoObras[i]);
        }
      }
      return catalogoFiltrado;
    },
  },
  beforeMount() {
    if (localStorage.Categoria != "[]") {
      this.categorias = JSON.parse(localStorage.getItem("Categoria"));
    }
    if (localStorage.Catalogo != "[]") {
      this.catalogoObras = JSON.parse(localStorage.getItem("Catalogo"));
    }
  },
  methods: {
    descCategoria() {
      console.log(this.categorias.length);
      for (let i = 0; i < this.categorias.length; i++) {
        if (this.categorias[i].titulo == this.selectedItems)
          return this.categorias[i].mensaje;
      }
    },
  },
};
</script>

<style scoped>
.fondo {
  background-image: url(https://c.wallhere.com/photos/f9/5b/abstract_3D_texture_dark_digital_art-1904637.jpg!d);
  background-size: cover;
  background-attachment: fixed;
  background-repeat: no-repeat;
}

h1 {
  color: rgb(154, 34, 175);
  font-weight: bold;
  font-size: 3rem;
  font-style: italic;
  padding: 1.5rem 0rem;
}

h2 {
  color: white;
  font-size: 2rem;
  font-style: italic;
  margin: 0px 20px;
}

.card-desc {
  margin: 20px;
  background-color: rgb(111, 111, 111);
}

.titulo {
  color: brown;
  margin-left: 2rem;
  font-weight: bold;
  font-size: 1.5rem;
}

p {
  font-size: 1.2rem;
  line-height: 0.8;
}
span {
  font-weight: bold;
}

.v-card {
  background-color: rgb(226, 226, 226);
}

.titulo-desc {
  color: rgb(62, 62, 62);
}

.parr-desc {
  padding: 0px 2%;
  color: rgb(118, 118, 118);
  font-size: 1.2rem;
  line-height: 1.2;
}
</style>
