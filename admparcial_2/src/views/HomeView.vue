<template>
  <div class="home">    
    <HomePage msg="Estamos en el Home."/>
  </div>
</template>

<script>
// @ is an alias to /src
import HomePage from '@/components/HomePage.vue'

export default {
  name: 'HomeView',
  components: {
    HomePage
  }
}
</script>
