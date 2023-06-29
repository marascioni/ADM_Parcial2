<template>
  <div class="cardObra">    
    <v-card class="mx-auto" max-width="360">
      <v-card-title class="titulo">{{ obra.nombre }}</v-card-title>    
      <v-img :src="'https://parcial2adm.000webhostapp.com/archivos/'+obra.portada" :alt="obra.alt" 
      contain max-height="250px" class="mx-auto"></v-img>
      <v-expand-transition>
        <div>
          <v-card-text>
          <p hidden>{{obra.id}}</p>
            <p><span>Autor:</span> {{ obra.autor }}</p>
            <p><span>Categoría:</span> {{ obra.categoria }}</p>
            <p><span>Estilo:</span> {{ obra.estilo }}</p>
            <p :class="`rounded white--text font-weight-${(obra.anio < 1950) ? 'black cyan' : 'regular indigo'}` "><span>Año:</span> {{ obra.anio }}</p>
          </v-card-text>            
            <v-icon large class="pb-4" v-if="$route.name!='home'" @click="borrar">{{"mdi-trash-can-outline"}}</v-icon>
                  
        </div>
      </v-expand-transition>
    </v-card>
    
  </div>
</template>

<script>

export default {
  name: "CardObra",
  props: {
    obra: Object,    
  },
  data: () => ({
    catalogoObras: [],    
  }),
  methods: {
    borrar(e){      
      //idObra a borrar
      this.$emit('borrado',e.target.parentElement.firstChild.firstChild.innerText);
    } ,  
  },
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
  line-height: 0.5;
  padding: 10px;  
}
</style>