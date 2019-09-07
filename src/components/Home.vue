<template>
  <v-card
    class="mx-auto"
    style="border-radious:0;"
  >
    <v-img
      class="white--text"
      height="100vh"
      src="@/assets/bg1.jpg"
    >
      <v-card-title style="margin-top: 25%;" class="align-center display-3">Welcome to Kip-Kip 
        <v-avatar>
          <img style="width:130%; height:auto;" src="@/assets/logo.png" alt="avatar">
        </v-avatar>
        <v-card-text>
          Your #1 Time Manager
        </v-card-text>
        <Registration/>
      </v-card-title>
    </v-img>
  </v-card>
</template>

<script>
import Registration from "./Registration"
export default {
  data: () => ({
    
  }),
  components:{
    Registration
  }
};
</script>