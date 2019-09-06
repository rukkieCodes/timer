<template>
  <v-app id="app">
    <Home/>
  </v-app>
</template>

<script>
import Home from "./views/Home"
export default {
  name: 'App',
  components:{
    Home
  }
};
</script>