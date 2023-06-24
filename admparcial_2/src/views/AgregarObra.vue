<template>
  <div class="home">    
    <NuevaObra msg="Estamos agregando una nueva obra."/>
  </div>
</template>

<script>
// @ is an alias to /src
import NuevaObra from '@/components/NuevaObra.vue'

export default {
  name: 'AgregarObra',
  components: {
    NuevaObra
  }
}
</script>
