<template>
  <div id="app">
    <v-app>
      <v-app-bar height="80px" >
        <v-app-bar-nav-icon class="pb-4" @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
      </v-app-bar>
      <v-navigation-drawer v-model="drawer" absolute left temporary>
        <v-list-item @click="showDialog">
          <v-list-item-content>
            <v-container fluid>
              <v-img
                src="../public/img/logo/logo_ok.png"
                class="mx-auto"
                width="80px"
              >
              </v-img>
            </v-container>
            <v-list-item-title class="text-h5 text-center font-weight-black font-italic" > SauRa </v-list-item-title>
            <v-list-item-subtitle class="text-h7 text-center">
              {{ sesion ? "Cerrar sesión" : "Iniciar sesión" }} 
            </v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>

        <v-divider></v-divider>

        <v-list dense nav>
          <v-list-item v-for="item in authorizedItems" :key="item.title" link>
            <v-list-item-icon>
              <v-icon>{{ item.icon }}</v-icon>
            </v-list-item-icon>

            <v-list-item-content>
              <v-list-item-title>
                <router-link :to="item.link" class="link" >
                  {{ item.title }}
                </router-link>
              </v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </v-list>
      </v-navigation-drawer>

      <v-snackbar v-model="snackbarError" timeout="5000" top color="error">
        {{ textError }}

        <template v-slot:action="{ attrs }">
          <v-btn
            color="white"
            text
            v-bind="attrs"
            @click="snackbarError = false"
          >
            Cerrar
          </v-btn>
        </template>
      </v-snackbar>

      <template>
        <v-row justify="center">
          <v-dialog v-model="dialog" persistent max-width="600px">
            <template v-slot:activator="{}"> </template>
            <v-card>
              <v-card-title>
                <span class="text-h5 pt-4 mx-auto font-italic font-weight-black text-color" >Inicio de sesión</span>
              </v-card-title>
              <v-card-text>
                <v-container >
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
                      <v-checkbox
                        v-model="termCond"
                        label="Términos y condiciones*"
                      ></v-checkbox>
                    </v-col>
                  </v-row>
                </v-container>
                <small>*campos obligatorios</small>
              </v-card-text>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="purple darken-2" text @click="dialog = false">
                  Cerrar
                </v-btn>
                <v-btn color="purple darken-2" text @click="login">
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
import { initializeApp } from "firebase/app";

const firebaseConfig = {
  apiKey: "AIzaSyCPQ5aEfJ5WA6hq9HQT4KXY03VwTna2cLs",
  authDomain: "adm-parcial2.firebaseapp.com",
  projectId: "adm-parcial2",
  storageBucket: "adm-parcial2.appspot.com",
  messagingSenderId: "1062042767340",
  appId: "1:1062042767340:web:73eba1582192d27f3f7ac9",
};
const app = initializeApp(firebaseConfig);
import { getAuth, signInWithEmailAndPassword, signOut } from "firebase/auth";
const auth = getAuth(app);

export default {
  name: "App",
  data: () => ({
    //dialog login
    sesion: false,
    email: "",
    password: "",
    termCond: false,
    dialog: false,
    snackbarError: false,
    textError: "Verifique los datos cargados",
    ///
    drawer: false,
    items: [
      { title: "Home", icon: "mdi-home", link: "/", authRequired: false },
      {
        title: "Nueva Obra",
        icon: "mdi-image",
        link: "/agregar",
        authRequired: true,
      },
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
        id: 1,
        nombre: "Agoo",
        portada: "pin104.jpg",
        alt: "Pintura Agoo",
        categoria: "Pintura",
        categ: 1,
        anio: 1965,
        estilo: "Abstracción",
        autor: "Silva Carlos Ismael",
      },
      {
        id: 2,
        nombre: "El conventillo",
        portada: "div201.jpg",
        alt: "Dibujo El conventillo",
        categoria: "Dibujo",
        categ: 2,
        anio: 1930,
        estilo: "Realismo",
        autor: "Facio Hebequer Guillermo",
      },
      {
        id: 3,
        nombre: "El mudo",
        portada: "esc303.jpg",
        alt: "Dibujo El mudo",
        categoria: "Escultura",
        categ: 3,
        anio: 1973,
        estilo: "Nueva figuración",
        autor: "Distéfano Juan Carlos",
      },
      {
        id: 4,
        nombre: "Buenos Aires nocturno",
        portada: "fot401.jpg",
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
  computed: {
    authorizedItems() {
      return this.items.filter((item) => !item.authRequired || this.sesion);
    },
  },
  methods: {
    login() {
      if (!this.sesion && this.termCond) {
        signInWithEmailAndPassword(auth, this.email, this.password)
          .then((userCredential) => {
            // Signed in
            const user = userCredential.user;
            console.log(user.displayName);
            this.sesion = true;
            this.dialog = false;
          })
          .catch((error) => {
            const errorCode = error.code;
            const errorMessage = error.message;
            console.log(errorMessage);
            this.snackbarError = true;
            if (errorCode == "auth/user-not-found")
              this.textError = "El email cargado no existe";
            if (errorCode == "auth/wrong-password")
              this.textError = "El password ingresado es incorrecto";
          });
      } else {
        this.snackbarError = true;
        this.textError = "Falta aceptar los terminos y condiciones";
      }
    },
    showDialog() {
      if (!this.sesion) {
        this.dialog = true;
      } else {
        signOut(auth)
          .then(() => {
            // Sign-out successful.
          })
          .catch((error) => {
            // An error happened.
            console.log(error);
          });
        this.sesion = false;
        this.termCond = false;
        if (this.$route.name == "agregar") this.$router.push("/");
      }
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  //text-align: center;
  color: #462c50;
  text-decoration: none;
}

.text-color{
  color: rgb(154, 34, 175);
}

.link{
  text-decoration: none;  
  color: black!important;
  font-weight: bold;
}
</style>
