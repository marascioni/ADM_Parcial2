<template>
  <div id="app">
    <v-app>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>

      <v-navigation-drawer v-model="drawer" absolute left temporary>
        <v-list-item @click="showDialog">
          <v-list-item-content>
            <v-list-item-title class="text-h6"> SauRa </v-list-item-title>
            <v-list-item-subtitle> Inicio sesión </v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>

        <v-divider></v-divider>

        <v-list dense nav>
          <v-list-item v-for="item in items" :key="item.title" link>
            <v-list-item-icon>
              <v-icon>{{ item.icon }}</v-icon>
            </v-list-item-icon>

            <v-list-item-content>
              <v-list-item-title>
                <router-link :to="item.link">
                  {{ item.title }}
                </router-link>
              </v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </v-list>
      </v-navigation-drawer>



      <template>
        <v-row justify="center">
          <v-dialog v-model="dialog" persistent max-width="600px">
            <template v-slot:activator="{ }">
              <v-btn></v-btn>
            </template>
            <v-card>
                  <v-card-title>
                    <span class="text-h5">Inicio de sesión</span>
                  </v-card-title>
                  <v-card-text>
                    <v-container>
                      <v-row>
                        <v-col cols="12">
                          <v-text-field
                            v-model="email"
                            label="Email*"
                            required
                          ></v-text-field>
                        </v-col>
                        <v-col cols="12">
                          <v-text-field
                            v-model="password"
                            label="Password*"
                            type="password"
                            required
                          ></v-text-field>
                        </v-col>
                        <v-col cols="12">
                          <v-checkbox label="Politicas de privacidad*"></v-checkbox>
                          <v-checkbox label="Términos y condiciones*"></v-checkbox>
                        </v-col>
                      </v-row>
                    </v-container>
                    <small>*campos obligatorios</small>
                  </v-card-text>
                  <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn color="blue darken-1" text @click="dialog = false">
                      Cerrar
                    </v-btn>
                    <v-btn color="blue darken-1" text @click="login">
                      Iniciar Sesión
                    </v-btn>
                  </v-card-actions>
                </v-card>
          </v-dialog>
        </v-row>
      </template>

      <v-main>
        <router-view />
      </v-main>
    </v-app>
  </div>
</template>

<script>
export default {
  name: "App",
  data: () => ({
    //dialog login
    email:"",
    password:"",
    dialog:false, 
    ///
    drawer: false,
    items: [
      { title: "Home", icon: "mdi-home", link: "/" },
      { title: "Nueva Obra", icon: "mdi-image", link: "/agregar" },      
    ],  
    categorias: [
      {
        id: 1,
        titulo: "Pintura",
        mensaje:
          "Cuando miramos una obra de arte estamos sometidos al recuerdo de una multitud de cosas que para bien o para mal influyen sobre nuestros gustos. (Gombrich)",
      },
      {
        id: 2,
        titulo: "Dibujo",
        mensaje:
          "Se considera al dibujo como el lenguaje gráfico universal y ha sido utilizado por la humanidad para transmitir ideas, proyectos y en un sentido más amplio.",
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
  /*******************************************/
  /* METODOS */
  /*******************************************/
  beforeMount() {
    console.log("Se va a montar el componente");
    if (localStorage.Catalogo != undefined) {
      this.catalogoObras = JSON.parse(localStorage.getItem("Catalogo"));
    } else {
      localStorage.setItem("Catalogo", JSON.stringify(this.catalogoObras));
    }
    if (localStorage.Categoria != undefined) {
      this.categorias = JSON.parse(localStorage.getItem("Categoria"));
    } else {
      localStorage.setItem("Categoria", JSON.stringify(this.categorias));
    }
  },
  methods: {
    login() {
      console.log("hola");
    },
    showDialog(){
      console.log("login");
      this.dialog=true;
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #462c50;
}

nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
