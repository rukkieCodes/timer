<template>
  <v-container fluid class="my-8">
    <v-flex>
      <div class="text-center">
        <v-avatar size="110">
          <img class="logo" src="@/assets/logo.png" alt="avatar" />
        </v-avatar>
      </div>
    </v-flex>
    <v-row>
      <v-col cols="12" md="6">
        <v-sheet elevation="2" class="pa-12">
          <v-text-field placeholder="What needs to be done" v-model="model"></v-text-field>
          <div class="mt-12 text-center">{{ model }}</div>
        </v-sheet>
      </v-col>
    </v-row>
  </v-container>
</template>


<script>
export default {
  data: () => ({
    model: ""
  })
};
</script>

<style lang="scss" scoped>
.logo {
  position: absolute;
  animation: spin 4s linear infinite;
}
@keyframes spin {
  100% {
    -webkit-transform: rotate(360deg);
    transform: rotate(360deg);
  }
}
</style>