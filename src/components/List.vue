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
          ></v-text-field>

          <v-layout class="mt-5 text-left" v-for="(todo, index) in todos" :key="todo.id">
            <v-flex>
              <v-checkbox v-model="todo.completed"></v-checkbox>
            </v-flex>
            <v-flex
              v-if="!todo.editing"
              @dblclick="editTodo(todo)"
              class="text-left animated bounceInUp"
              :class="{ completed : todo.completed }"
            >
              <p>{{ todo.title }}</p>
            </v-flex>
            <!-- <input v-else type="text" v-model="todo.title" /> -->
            <v-flex v-else>
              <v-text-field
                type="text"
                v-model="todo.title"
                @blur="doneEditing(todo)"
                @keyup.enter="doneEditing(todo)"
                @keyup.esc="cancelEditing(todo)"
                v-focus
              ></v-text-field>
            </v-flex>
            <v-flex class="text-right">
              <i @click="editTodo(todo)" class="primary--text fa fa-pen mr-5"></i>
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
    beforeEditCache: "",
    todos: [
      {
        id: 1,
        title: "yajnnb",
        completed: false,
        editing: false
      },
      {
        id: 2,
        title: "yolo",
        completed: false,
        editing: false
      }
    ]
  }),
  directives: {
    focus: {
      inserted: function(el) {
        el.focus();
      }
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim().length == 0) {
        return;
      }

      this.todos.push({
        id: this.idForTodo,
        title: this.newTodo,
        completed: false
      });

      this.newTodo = "";
      this.idForTodo++;
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    },
    editTodo(todo) {
      this.beforeEditCache = todo.title;
      todo.editing = true;
    },
    doneEditing(todo) {
      if (todo.title.trim() == "") {
        todo.title = this.beforeEditCache;
      }
      todo.editing = false;
    },
    cancelEditing(todo) {
      todo.title = this.beforeEditCache;
      todo.editing = false;
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

.completed{
    text-decoration: line-through;
    color: grey;
}
</style>