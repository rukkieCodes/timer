<template>
  <v-layout>
      <v-flex>
          <Nav/>
      </v-flex>
      <v-flex>
          <List/>
      </v-flex>
  </v-layout>
</template>

<script>
import Nav from "../components/Nav"
import List from "../components/List"
export default {
    components:{
        Nav,
        List
    }
}
</script>