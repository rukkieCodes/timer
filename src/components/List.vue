<template>
  <v-container fluid class="my-8">
    <v-row>
      <v-col cols="12">
        <v-sheet elevation="5" class="pa-12 ma-auto">
          <v-text-field
            placeholder="What needs to be done"
            v-model="newTodo"
            @keyup.enter="addTodo"
          ></v-text-field>

          <v-layout class="extra-container" wrap row>
            <v-flex >
              <input name="checkAll" type="checkbox" :checked="!anyRemaining" @change="checkAllTodos"/>
              <label for="checkAll">Check All</label>
            </v-flex>
            <v-flex class="text-right">
              <div>{{ remaining }} items left</div>
            </v-flex>
          </v-layout>

          <v-layout class="extra-container" wrap row>
            <v-flex >
              <v-btn class="button" :class="{ active: filter == 'all' }" @click="filter = 'all'">All</v-btn>
            </v-flex>
            <v-flex class="text-right">
              <v-btn class="button" :class="{ active: filter == 'active' }" @click="filter = 'active'">Active</v-btn>
            </v-flex>
            <v-flex>
              <v-btn class="button" :class="{ active: filter == 'completed' }" @click="filter = 'completed'">Completed</v-btn>
            </v-flex>
            <v-flex>
              <v-btn v-if="showClearCompletedButton" @click="clearCompleted">Clear Completed</v-btn>
            </v-flex>
          </v-layout>



          <v-layout row wrap class="container text-left" v-for="(todo, index) in todosFilted" :key="todo.id">
            <v-flex>
              <input type="checkbox" v-model="todo.completed"/>
            </v-flex>
            <v-flex
              v-if="!todo.editing"
              @dblclick="editTodo(todo)"
              class="text-left"
              :class="{ completed : todo.completed }"
            >
              <p>{{ todo.title }}</p>
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
        </v-sheet>
      </v-col>
    </v-row>
  </v-container>
</template>


<script>
export default {
  data: () => ({
    bottomNav: "recent",
    newTodo: "",
    idForTodo: 3,
    beforeEditCache: "",
    filter: 'all',
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
  computed:{
    remaining(){
      return this.todos.filter(todo => !todo.completed).length
    },
    anyRemaining(){
      return this.remaining != 0
    },
    todosFilted(){
      if(this.filter == 'all'){
        return this.todos
      }else if(this.filter == 'active'){
        return this.todos.filter(todo => !todo.completed)
      }else if(this.filter == 'completed'){
        return this.todos.filter(todo => todo.completed)
      }

      return this.todos
    },
    showClearCompletedButton(){
      return this.todos.filter(todo => todo.completed).length > 0
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

      this.newTodo = ''
      this.idForTodo++
    },
    editTodo(todo) {
      this.beforeEditCache = todo.title;
      todo.editing = true;
    },
    doneEditing(todo) {
      if (todo.title.trim() == '') {
        todo.title = this.beforeEditCache;
      }
      todo.editing = false
    },
    cancelEditing(todo) {
      todo.title = this.beforeEditCache;
      todo.editing = false;
    },
    removeTodo(index) {
      this.todos.splice(index, 1)
    },
    checkAllTodos(){
      this.todos.forEach((todo) => todo.completed = event.target.checked)
    },
    clearCompleted(){
      this.todos = this.todos.filter(todo => !todo.completed)
    }
  }
}
</script>

<style lang="scss" scoped>
.completed {
  text-decoration: line-through;
  color: grey;
}
.extra-container{
  display: flex;
  align-items: center;
  justify-content: space-around;
  padding: 14px;
}
.container{
  display: flex;
  align-items: center;
  justify-content: start;
}
.button{
  font-size: 14px;
  background: #fff;
  appearance: none;

  &:hover{
    background: lightgreen;
  }

  &:focus{
    outline: none;
  }
}

.active{
  background: lightgreen;
}
</style>