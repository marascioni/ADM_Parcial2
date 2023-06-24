<template>
  <v-footer dark padless class="mt-6">
    <v-col>
      <v-card flat tile class="lighten-1 white--text text-center">
        <v-card-text>
          <v-btn v-for="icon in socialNet" :key="icon.icon" class="mx-4 white--text" icon :href="icon.link"  target="_blank">
            <v-icon size="24px">
              {{ icon.icon }}              
            </v-icon>
          </v-btn>
        </v-card-text>

        <v-card-text class="white--text pt-0">
          Rascioni Miguel - Saurrales Carolina - 2023 - Aplicación para
          dispositivos móviles - DWN2CV
        </v-card-text>    
      </v-card>
    </v-col>
  </v-footer>
</template>

<script>
export default {
  name: "FooterPage",
  props: {
    msg: String,
  },
  data: () => ({
    socialNet: [
    {icon: "mdi-facebook", link:"https://es-la.facebook.com/"}, 
    {icon: "mdi-twitter", link:"https://www.twitter.com/"}, 
    {icon: "mdi-whatsapp", link:"https://api.whatsapp.com/send?phone=01159628124"}, 
    {icon: "mdi-instagram", link:"https://www.instagram.com/"}],
  }),
};
</script>
