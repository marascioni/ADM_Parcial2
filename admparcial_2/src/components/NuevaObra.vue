<template>
  <div id="nuevaObra" class="mx-auto fond">
    <div class="text-center">
      <h1>Nueva Obra</h1>
    </div>
    <v-item-group>
      <v-container>
        <v-row>
          <v-col cols="12" md="4">
            <v-item>
              <v-img src="../../public/img/logo/logo_ok.png" width="100%">
              </v-img>
            </v-item>
          </v-col>
          <v-col cols="12" md="6">
            <v-item>
              <form class="mx-10">
                <v-text-field
                  class="input-field"
                  v-model="titulo"
                  label="Título"
                  required
                  @input="$v.titulo.$touch()"
                  @blur="$v.titulo.$touch()"
                ></v-text-field>
                <v-text-field
                  v-model="imagen"
                  label="Imagen"
                  required
                  @input="$v.imagen.$touch()"
                  @blur="$v.imagen.$touch()"
                ></v-text-field>
                <v-text-field
                  v-model="altImg"
                  label="Texto Alternativo"
                  required
                  @input="$v.altImg.$touch()"
                  @blur="$v.altImg.$touch()"
                ></v-text-field>
                <v-text-field
                  v-model="anio"
                  label="Año obra"
                  required
                  @input="$v.anio.$touch()"
                  @blur="$v.anio.$touch()"
                ></v-text-field>
                <v-text-field
                  v-model="estilo"
                  label="Estilo"
                  required
                  @input="$v.estilo.$touch()"
                  @blur="$v.estilo.$touch()"
                ></v-text-field>
                <v-text-field
                  v-model="artista"
                  label="Artista"
                  required
                  @input="$v.artista.$touch()"
                  @blur="$v.artista.$touch()"
                ></v-text-field>

                <v-select
                  v-model="categoria"
                  :items="listarCategoria"
                  label="Categoría"
                  required
                  @change="$v.select.$touch()"
                  @blur="$v.select.$touch()"
                ></v-select>

                <v-btn class="mr-4" @click="submit"> Agregar </v-btn>
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
    name: "",
    email: "",
    select: null,
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
    items: ["Item 1", "Item 2", "Item 3", "Item 4"],
  }),
  props: {
    msg: String,
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
  color: rebeccapurple;
}

.v-label { color: rgb(255, 0, 0) !important; }

</style>
