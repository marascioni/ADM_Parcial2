<template>
  <div class="fondo">
    <h1>Obras</h1>

    <v-col class="d-flex" cols="12" sm="6">
      <h2>Filtro</h2>
      <v-select
        class="dropdown"
        v-model="selectedItems"
        :items="listarCategoria"
        solo
      ></v-select>
    </v-col>

    <v-card class="mx-auto card-desc" max-width="60%" v-if="selectedItems != 'Catálogo'"
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
            v-for="obra in catalogoObras"
            :key="obra.nombre"
            cols="12"
            md="4"
          >
            <v-item
              v-if="
                selectedItems == obra.categoria || selectedItems == 'Catálogo'
              "
            >
              <v-card class="mx-auto" max-width="360">
                <v-card-title class="titulo">{{ obra.nombre }}</v-card-title>
                <v-img
                  :src="obra.portada"
                  :alt="obra.alt"
                  height="200px"
                ></v-img>
                <v-expand-transition>
                  <div>
                    <v-divider></v-divider>

                    <v-card-text>
                      <p><span>Autor:</span> {{ obra.autor }}</p>
                      <p><span>Categoría:</span> {{ obra.categoria }}</p>
                      <p><span>Estilo:</span> {{ obra.estilo }}</p>
                      <p><span>Año:</span> {{ obra.anio }}</p>
                    </v-card-text>
                  </div>
                </v-expand-transition>
              </v-card>
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

export default {
  name: "NuevaObra",
  components: {
    FooterPage,
  },
  data: () => ({
    show: true,
    selectedItems: "Catálogo",
    categorias: [
      {
        id: 1,
        titulo: "Pintura",
        mensaje:
          "“Cuando miramos una obra de arte estamos sometidos al recuerdo de una multitud de cosas que para bien o para mal influyen sobre nuestros gustos“. (Gombrich)",
      },
      {
        id: 2,
        titulo: "Dibujo",
        mensaje:
          "“Se considera al dibujo como el lenguaje gráfico universal y ha sido utilizado por la humanidad para transmitir ideas, proyectos y en un sentido más amplio“.",
      },
      {
        id: 3,
        titulo: "Escultura",
        mensaje:
          "Incluye todas las artes de talla y cincel, junto con las de fundición y moldeado. ... “El escultor saca todo lo superfluo y reduce el material a la forma que existe dentro de la mente del artista“.",
      },
      {
        id: 4,
        titulo: "Fotografía",
        mensaje:
          "“La fotografia es un secreto de un secreto. Cuanto mas te dice, menos sabes“ (Diane Arbus).  «Lo más importante no es la cámara, sino el ojo.» (Alfred Eisenstaedt)",
      },
    ],
    catalogoObras: [
      {
        nombre: "Agoo",
        portada: "img/pin104.jpg",
        alt: "Pintura Agoo",
        categoria: "Pintura",
        categ: 1,
        anio: 1965,
        estilo: "Abstracción",
        autor: "Silva Carlos Ismael",
      },
      {
        nombre: "El conventillo",
        portada: "img/div201.jpg",
        alt: "Dibujo El conventillo",
        categoria: "Dibujo",
        categ: 2,
        anio: 1930,
        estilo: "Realismo",
        autor: "Facio Hebequer Guillermo",
      },
      {
        nombre: "El mudo",
        portada: "img/esc303.jpg",
        alt: "Dibujo El mudo",
        categoria: "Escultura",
        categ: 3,
        anio: 1973,
        estilo: "Nueva figuración",
        autor: "Distéfano Juan Carlos",
      },
      {
        nombre: "Buenos Aires nocturno",
        portada: "img/fot401.jpg",
        alt: "Fotografía Buenos Aires nocturno",
        categoria: "Fotografía",
        categ: 4,
        anio: 1936,
        estilo: "Realismo",
        autor: "Coppola Horacio",
      },
    ],
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

.dropdown {
  color: white;
  background-color: white;
  max-width: 200px;
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

.card-desc {
  margin: 20px;
  background-color: rgb(111, 111, 111);
}

.titulo-desc {
  color: white;
}
.parr-desc {
  padding: 0px 2%;
  color: white;
  font-size: 1.2rem;
  line-height: 1.2;
}
</style>
