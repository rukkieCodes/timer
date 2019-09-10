<v-container fluid class="my-8">
    <v-row>
      <v-col class="columns" cols="12">
        <v-text-field placeholder="What needs to be done" v-model="newTodo" @keyup.enter="addTodo"></v-text-field>
        <v-layout class="extra-container" wrap row>
          <v-flex>
            <input name="checkAll" type="checkbox" :checked="!anyRemaining" @change="checkAllTodos" />
            <label for="checkAll">Check All</label>
          </v-flex>
          <v-flex class="text-right">
            <div>{{ remaining }} items left</div>
          </v-flex>
        </v-layout>

        <v-layout class="extra-container" wrap row>
          <v-flex>
            <v-btn class="button" :class="{ active: filter == 'all' }" @click="filter = 'all'">All</v-btn>
          </v-flex>
          <v-flex class="text-right">
            <v-btn
              class="button"
              :class="{ active: filter == 'active' }"
              @click="filter = 'active'"
            >Active</v-btn>
          </v-flex>
          <v-flex>
            <v-btn
              class="button"
              :class="{ active: filter == 'completed' }"
              @click="filter = 'completed'"
            >Completed</v-btn>
          </v-flex>
          <v-flex>
            <v-btn v-if="showClearCompletedButton" @click="clearCompleted">Clear Completed</v-btn>
          </v-flex>
        </v-layout>

        <v-layout
          row
          wrap
          class="container text-left"
          v-for="(todo, index) in todosFilted"
          :key="todo.id"
        >
          <v-flex>
            <input type="checkbox" v-model="todo.completed" />
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
      </v-col>
    </v-row>
  </v-container>