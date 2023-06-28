<template>
  <div class="cardObra">    
    <v-card class="mx-auto" max-width="360">
      <v-card-title class="titulo">{{ obra.nombre }}</v-card-title>
      <v-img :src="'https://parcial2adm.000webhostapp.com/archivos/'+obra.portada" :alt="obra.alt" height="200px"></v-img>
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
    
  </div>
</template>

<script>
export default {
  name: "CardObra",
  props: {
    obra: Array,    
  },
  data: () => ({
    
  }),
};
</script>

<style scoped>
.titulo {
  color: brown;
  margin-left: 2rem;
  font-weight: bold;
  font-size: 1.5rem;
}

span {
  font-weight: bold;
}

.v-card {
  background-color: rgb(226, 226, 226);
}

p {
  font-size: 1.2rem;
  line-height: 0.8;
}
</style>