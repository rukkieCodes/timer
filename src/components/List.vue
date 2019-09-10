<template>
  <v-container class="mt-5 container justify-center">
    <v-layout row wrap>
      <v-flex xs12 sm12 md12 lg12 xl12>
        <v-text-field placeholder="What needs to be done" v-model="newTodo" @keyup.enter="addTodo"></v-text-field>
      </v-flex>
      <v-flex xs6 sm6 md6 lg6 xl6 class="text-left">
        <input name="checkAll" type="checkbox" :checked="!anyRemaining" @change="checkAllTodos" />
        <label for="checkAll">Check All</label>
      </v-flex>
      <v-flex class="text-right">
        <div>{{ remaining }} items left</div>
      </v-flex>
    </v-layout>

    <v-layout wrap row>
      <v-flex xs6 sm6 md3 lg3 xl3>
        <v-btn class="button" :class="{ active: filter == 'all' }" @click="filter = 'all'">All</v-btn>
      </v-flex>
      <v-flex xs6 sm6 md3 lg3 xl3>
        <v-btn
          class="button"
          :class="{ active: filter == 'active' }"
          @click="filter = 'active'"
        >Active</v-btn>
      </v-flex>
      <v-flex xs6 sm6 md3 lg3 xl3>
        <v-btn
          class="button"
          :class="{ active: filter == 'completed' }"
          @click="filter = 'completed'"
        >Completed</v-btn>
      </v-flex>
      <v-flex xs6 sm6 md3 lg3 xl3>
        <v-btn
          class="button"
          v-if="showClearCompletedButton"
          @click="clearCompleted"
        >Clear Completed</v-btn>
      </v-flex>
    </v-layout>
    <v-divider></v-divider>

    <v-layout
      wrap
      row
      class="list text-left mt-5"
      v-for="(todo, index) in todosFilted"
      :key="todo.id"
    >
      <v-flex xs1 sm1 md1 lg1 xl1>
        <input type="checkbox" v-model="todo.completed" />
      </v-flex>
      <v-flex
        v-if="!todo.editing"
        @dblclick="editTodo(todo)"
        :class="{ completed : todo.completed }"
      >
        <p class="mt-3">{{ todo.title }}</p>
      </v-flex>
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
  </v-container>
</template>


<script>
export default {
  data: () => ({
    bottomNav: "recent",
    newTodo: "",
    idForTodo: 3,
    beforeEditCache: "",
    filter: "all",
    todos: [
      {
        id: 1,
        title: "Watch Football",
        completed: false,
        editing: false
      },
      {
        id: 2,
        title: "Go out for a walk",
        completed: false,
        editing: false
      }
    ]
  }),
  computed: {
    remaining() {
      return this.todos.filter(todo => !todo.completed).length;
    },
    anyRemaining() {
      return this.remaining != 0;
    },
    todosFilted() {
      if (this.filter == "all") {
        return this.todos;
      } else if (this.filter == "active") {
        return this.todos.filter(todo => !todo.completed);
      } else if (this.filter == "completed") {
        return this.todos.filter(todo => todo.completed);
      }

      return this.todos;
    },
    showClearCompletedButton() {
      return this.todos.filter(todo => todo.completed).length > 0;
    }
  },
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
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    },
    checkAllTodos() {
      this.todos.forEach(todo => (todo.completed = event.target.checked));
    },
    clearCompleted() {
      this.todos = this.todos.filter(todo => !todo.completed);
    }
  }
};
</script>

<style lang="scss" scoped>
.container {
  max-width: 100%;
  margin: auto;
  padding: 0 4%;
  height: 80vh;
  max-height: 80vh;
  overflow-y: scroll;
  border-bottom: 0.4px solid rgba(0,0,0,0.5);
  @media (min-width: 768px) {
    max-width: 50%;
  }
  &::-webkit-scrollbar {
    width: .7em;
  }
  &::-webkit-scrollbar-track {
    // -webkit-box-shadow: inset 0 0 6px rgba(0, 0, 0, 0.3);
  }
  &::-webkit-scrollbar-thumb {
    background-color: #4169e1;
    // outline: 1px solid slategrey;
  }

  .button {
    background: none !important;
    font-size: 0.7em;
    box-shadow: none;
  }
}
.completed {
  text-decoration: line-through;
  color: grey;
}
// .extra-container {
//   display: flex;
//   align-items: center;
//   justify-content: space-around;
//   padding: 14px;
// }
.list {
  display: flex;
  align-items: center;
  justify-content: start;
}
</style>