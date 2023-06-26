<template>
  <div class="cardObra">
    <h1>Obras agregada</h1>   
    <v-card class="mx-auto" max-width="360">
      <v-card-title class="titulo">{{ obra.nombre }}</v-card-title>
      <v-img :src="obra.portada" :alt="obra.alt" height="200px"></v-img>
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
