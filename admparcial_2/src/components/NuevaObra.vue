<template>
  <div id="nuevaObra" class="mx-auto fondo">
    <div class="text-center">
      <h1>Nueva Obra</h1>
    </div>

    <v-snackbar v-model="snackbarError" timeout="5000" top color="error">
      {{ textError }}

      <template v-slot:action="{ attrs }">
        <v-btn color="white" text v-bind="attrs" @click="snackbarError = false">
          Cerrar
        </v-btn>
      </template>
    </v-snackbar>

    <v-snackbar v-model="snackbarOk" timeout="5000" top color="success">
      {{ textOk }}

      <template v-slot:action="{ attrs }">
        <v-btn color="white" text v-bind="attrs" @click="snackbarOk = false">
          Cerrar
        </v-btn>
      </template>
    </v-snackbar>

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
                  label="Título*"
                  required
                ></v-text-field>
                <!-- <v-text-field
                  class="px-5"
                  v-model="portadaObra"
                  label="Imagen*"
                  required
                ></v-text-field>               -->
                <v-file-input
                  v-model="fichero"
                  class="px-5"
                  label="Imagen*"
                  type="file"
                  accept="image/*"
                  required
                ></v-file-input>
                <v-text-field
                  class="px-5"
                  v-model="altObra"
                  label="Texto Alternativo"
                ></v-text-field>
                <v-text-field
                  class="px-5"
                  v-model="anioObra"
                  label="Año obra*"
                  required
                ></v-text-field>
                <v-text-field
                  class="px-5"
                  v-model="estiloObra"
                  label="Estilo*"
                  required
                ></v-text-field>
                <v-text-field
                  class="px-5"
                  v-model="autorObra"
                  label="Artista*"
                  required
                ></v-text-field>

                <v-select
                  class="px-5"
                  v-model="categoriaSeleccionada"
                  :items="listarCategoria"
                  label="Categoría*"
                  required
                ></v-select>

                <v-btn class="mr-4 mb-4 secondary" @click="controlarCampos">
                  Agregar
                </v-btn>
              </form>
            </v-item>
          </v-col>
        </v-row>
      </v-container>
    </v-item-group>
    <v-item-group>
      <v-container v-if="nuevaObra.length">
        <h2>Obras agregadas</h2>
        <v-row>
          <v-col v-for="obra in nuevaObra" :key="obra.nombre" cols="12" md="4">
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
  name: "NuevaObra",
  components: {
    FooterPage,
    CardObra,
  },
  data: () => ({
    file: null,
    snackbarError: false,
    textError: `Error en el ingreso de datos`,
    snackbarOk: false,
    textOk: `Se agregó una nueva obra`,
    categoriaSeleccionada: "",
    tituloObra: "",
    errorTitulo: true,
    portadaObra: "",
    fichero: "",
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

  methods: {
    agregarObra: function () {
      const imgData = new FormData();
      imgData.append("file", this.fichero);

      const options = {
        method: "POST",
        mode: "cors",
        cache: "no-cache",
        body: imgData,       
      };
      fetch("https://parcial2adm.000webhostapp.com/carga.php", options)
        .then((response) => {
          console.log(response);
          response.json();
        })
        .then((data) => console.log(data))
        .catch((err) => {
          console.log(`Hubo un error: ${err}`);
        })
        .finally((final) => {
          // borra el loading
          console.log("ejecuto el finally", final);
        });
      this.obra = {
        nombre: this.tituloObra,
        portada: this.fichero.name,
        alt: this.altObra,
        categoria: this.categoriaSeleccionada,
        categ: this.idObra,
        anio: this.anioObra,
        estilo: this.estiloObra,
        autor: this.autorObra,
      };

      this.nuevaObra.push(this.obra);
      this.tituloObra = "";
      this.fichero = "";
      this.altObra = "";
      this.idObra = 0;
      this.anioObra = "";
      this.estiloObra = "";
      this.autorObra = "";
      this.categoriaSeleccionada = "Categoría*";
      this.catalogoObras = this.catalogoObras.concat(this.obra);
      localStorage.setItem("Catalogo", JSON.stringify(this.catalogoObras));
    },

    controlarCampos: function () {
      for (let i = 0; i < this.categorias.length; i++) {
        if (this.categorias[i].titulo == this.categoriaSeleccionada)
          this.idObra = this.categorias[i].id;
      }
      this.tituloObra != ""
        ? (this.errorTitulo = true)
        : (this.errorTitulo = false);
      this.fichero != ""
        ? (this.errorPortada = true)
        : (this.errorPortada = false);
      this.idObra != 0 ? (this.errorId = true) : (this.errorId = false);
      this.estiloObra != ""
        ? (this.errorEstilo = true)
        : (this.errorEstilo = false);
      this.autorObra != ""
        ? (this.errorAutor = true)
        : (this.errorAutor = false);
      if (this.anioObra != "") {
        if (this.anioObra >= 1 && this.anioObra <= 9999) {
          this.errorAnio = true;
        } else {
          this.errorAnio = false;
        }
      } else {
        this.errorAnio = false;
      }
      if (
        this.errorTitulo &&
        this.errorPortada &&
        this.errorId &&
        this.errorAnio &&
        this.errorEstilo &&
        this.errorAutor
      ) {
        this.agregarObra();
        this.snackbarOk = true;
      } else {
        this.snackbarError = true;
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

form {
  background-color: rgb(255, 255, 255);
}
</style>
