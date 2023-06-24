<template>
  <div id="nuevaObra" class="mx-auto fondo">
    <div class="text-center">
      <h1>Nueva Obra</h1>
    </div>
    <v-item-group>
      <v-container>
        <v-row>
          <v-col cols="12" md="4">
            <v-item class="text-center">
              <v-img
                src="../../public/img/logo/logo_ok.png"
                class="mx-auto"
                width="80%"
              >
              </v-img>
            </v-item>
          </v-col>
          <v-col cols="12" md="6">
            <v-item>
              <form class="mx-10 rounded-lg">
                <v-text-field
                  class="px-5"
                  v-model="tituloObra"
                  label="Título"
                  required
                ></v-text-field>
                <v-text-field
                  class="px-5"
                  v-model="portadaObra"
                  label="Imagen"
                  required
                ></v-text-field>
                <v-text-field
                  class="px-5"
                  v-model="altObra"
                  label="Texto Alternativo"
                  required
                ></v-text-field>
                <v-text-field
                  class="px-5"
                  v-model="anioObra"
                  label="Año obra"
                  required
                ></v-text-field>
                <v-text-field
                  class="px-5"
                  v-model="estiloObra"
                  label="Estilo"
                  required
                ></v-text-field>
                <v-text-field
                  class="px-5"
                  v-model="autorObra"
                  label="Artista"
                  required
                ></v-text-field>

                <v-select
                  class="px-5"
                  v-model="categoria"
                  :items="listarCategoria"
                  label="Categoría"
                  required
                ></v-select>

                <v-btn class="mr-4 mb-4 secondary" @click="agregarObra">
                  Agregar
                </v-btn>
              </form>
            </v-item>
          </v-col>
        </v-row>
      </v-container>
    </v-item-group>
  </div>
</template>

<script>
export default {
  name: "NuevaObra",
  data: () => ({
    tituloObra: "",
    errorTitulo: true,
    portadaObra: "",
    errorPortada: true,
    altObra: "",
    errorAlt: true,
    anioObra: "",
    errorAnio: true,
    estiloObra: "",
    errorEstilo: true,
    autorObra: "",
    errorAutor: true,
    idObra: 0,
    errorId: true,
    categoriaObra: "",
    categorias: [],
    obra: [],
    nuevaObra: [],
    catalogoObras: [],
  }),
  props: {
    msg: String,
  },
  //Lee de localStorage las Categorias para el dropdown de selección
  beforeMount() {
    if (localStorage.Categoria != "[]") {
      this.categorias = JSON.parse(localStorage.getItem("Categoria"));
    }
    if (localStorage.Catalogo != "[]") {
      this.catalogoObras = JSON.parse(localStorage.getItem("Catalogo"));
    }
  },
  computed: {
    listarCategoria() {
      var listCategoria = [];
      for (let i = 0; i < this.categorias.length; i++) {
        listCategoria.push(this.categorias[i].titulo);
      }
      return listCategoria;
    },
  },

  //Guarda en localStorage las obras agregadas
  beforeDestroy() {
    if (this.nuevaObra != []) {
      if (localStorage.Catalogo) {
        this.catalogoObras = JSON.parse(localStorage.getItem("Catalogo"));
      }
      this.catalogoObras = this.catalogoObras.concat(this.nuevaObra);
      localStorage.setItem("Catalogo", JSON.stringify(this.catalogoObras));
    }
  },

  methods: {
    agregarObra: function () {
      console.log("dentro de agregarObra");
      //this.categoriaObra = this.categorias[this.idObra - 1].titulo;
      for (let i = 0; i < this.categorias.length; i++) {
        if (this.categorias[i].titulo == this.categoria)
          this.idObra = this.categorias[i].id;
      }
      this.obra = {
        nombre: this.tituloObra,
        portada: this.portadaObra,
        alt: this.altObra,
        categoria: this.categoria,
        categ: this.idObra,
        anio: this.anioObra,
        estilo: this.estiloObra,
        autor: this.autorObra,
      };
      console.log(this.obra);
      this.nuevaObra.push(this.obra);
      this.tituloObra = "";
      this.portadaObra = "";
      this.altObra = "";
      this.idObra = 0;
      this.anioObra = "";
      this.estiloObra = "";
      this.autorObra = "";
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

form {
  background-color: rgb(255, 255, 255);
}
</style>
