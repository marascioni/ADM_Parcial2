<template>
  <div id="app">
    <v-app>
      <v-app-bar
        app
        color="secondary"
        dark
        >
        <nav>
          <router-link to="/">Información general</router-link> |
          <router-link to="/about">Mi perfil</router-link> |
          <router-link to="/contact">Configuraciones</router-link>
        </nav>
      </v-app-bar>
      <v-main>
        <router-view />
      </v-main>
    </v-app>
  </div>
</template>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
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
