<template>
  <v-container>
    <div>
      <v-flex>
        <Nav />
      </v-flex>
      <v-flex>
        <List />
      </v-flex>
    </div>
  </v-container>
</template>

<script>
import Nav from "../components/Nav";
import List from "../components/List";
export default {
  components: {
    Nav,
    List
  }
};
</script>