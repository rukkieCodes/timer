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
          <v-text-field 
          placeholder="What needs to be done" 
          v-model="newTodo"
          @keyup.enter="addTodo"
          >
          </v-text-field>

          <!-- <v-flex class="mt-12 text-left" v-for="todo in todos" :key="todo.id">
              <p class="text-left">{{ todo.title }}</p>
              <i class="fa fa-times"></i>
          </v-flex> -->
          <v-layout class="mt-5 text-left" v-for="(todo, index) in todos" :key="todo.id">
              <v-flex class="text-left">
                  {{ todo.title }}
              </v-flex>
              <v-flex class="text-right">
                  <i @click="removeTodo(index)" class="red--text fa fa-trash"></i>
              </v-flex>
          </v-layout>
        </v-sheet>
      </v-col>
    </v-row>
  </v-container>
</template>


<script>
export default {
  data: () => ({
    newTodo: "",
    idForTodo: 3,
    todos:[]
  }),
  methods:{
      addTodo(){
          if(this.newTodo.trim().length == 0){
              return
          }

          this.todos.push({
              id: this.idForTodo,
              title: this.newTodo,
              completed: false
          })

          this.newTodo = ''
          this.idForTodo++
      },
      removeTodo(index){
          this.todos.splice(index, 1)
      }
  }
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