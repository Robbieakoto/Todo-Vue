<template>
  <div>
    <div id="AddTask">
      <div class="row" style="margin-top:100px; ">
        <div class="col-2 col-md-1 col-lg-2"></div>
        <div class="col-8 col-md-9 col-lg-7">
          <div class="line">
            <input
              type="text"
              class="text-line"
              placeholder="What do you need to do?"
              v-model="newTodo"
              @keyup.enter="addTodo"
              maxlength="30"
            />
          </div>
          <div class="col-2 col-md-3"></div>
        </div>
      </div>
    </div>

    <div class="favourite">
      <div class="row">
        <div class="col-1 col-md-1 col-lg-2"></div>

        <div class="col-10 col-md-9 col-lg-7">
          <div id="favourite">
            <p>
              <b>Favourites</b>
            </p>
          </div>

          <div
            class="card bg-light"
            style="margin-bottom:10px;"
            v-for="todo in todos.slice().reverse()"
            v-if="todo.favourite"
            :key="todo.id"
          >
            <div class="row" style="padding:8px;">
              <div class="col-8 col-md-10 col-lg-10">
                <span style="float:left;">{{ todo.title }}</span>
              </div>
              <div class="col-4 offset-0 col-md-2 offset-md-0 col-lg-2 offset-lg-0">
                <span id="clickableAwesomeFont">
                  <i class="fa fa-star" v-on:click="unStar(todo)"></i>
                </span>&nbsp;&nbsp;&nbsp;
                <span id="clickableAwesomeFont">
                  <i class="fa fa-trash" v-on:click="removeTodo(todo)"></i>
                </span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="Tasks" style="margin-top:10px;">
      <div class="row">
        <div class="col-1 col-md-1 col-lg-2"></div>

        <div class="col-10 col-md-9 col-lg-7">
          <div id="tasks">
            <p>
              <b>Tasks</b>
            </p>
          </div>
          <!-- eslint-disable vue/no-use-v-if-with-v-for,vue/no-confusing-v-for-v-if -->
          <div
            class="card bg-light"
            style="margin-bottom:10px;"
            v-if="!todo.favourite"
            v-for="todo in todos.slice().reverse()"
            :key="todo.id"
          >
            <div class="row" style="padding:6px;">
              <div class="col-8 col-md-10 col-lg-10">
                <span style="float:left;">{{ todo.title }}</span>
              </div>
              <div class="col-4 offset-0 col-md-2 offset-md-0 col-lg-2 offset-lg-0">
                <span id="clickableAwesomeFont">
                  <i class="fa fa-star-o" v-on:click="star(todo)"></i>
                </span>&nbsp;&nbsp;
                <span id="clickableAwesomeFont">
                  <i class="fa fa-trash" v-on:click="removeTodo(todo)"></i>
                </span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
const STORAGE_KEY = "todoist"; //storage key

const todoStorage = {
  //save todo list
  fetch: () => {
    //get items in the storage key
    const todos = JSON.parse(localStorage.getItem(STORAGE_KEY) || "[]");

    //loop through the todos using index
    todos.forEach((todo, index) => {
      //store the index as an id in a variable
      todo.id = index;
    });

    //store the length of todos and return the list
    todoStorage.uid = todos.length;

    return todos.slice().reverse();
  },
  save: todos => {
    localStorage.setItem(STORAGE_KEY, JSON.stringify(todos));
  }
};

export default {
  name: "AddTask",

  data: function() {
    return {
      todos: todoStorage.fetch(),
      newTodo: ""
    };
  },
  methods: {
    addTodo: function() {
      const todoValue = this.newTodo && this.newTodo.trim();

      if (!todoValue) {
        return;
      }

      this.todos.push({
        id: todoStorage.uid++,
        title: todoValue,
        favourite: false,
        completed: false
      });

      this.newTodo = " ";
    },

    removeTodo: function(todo) {
      this.todos.splice(this.todos.indexOf(todo), 1);
    },
    star: function(todo) {
      todo.favourite = true;
    },
    unStar: function(todo) {
      todo.favourite = false;
    }
  },
  watch: {
    todos: {
      handler: function(todos) {
        todoStorage.save(todos);
      },
      deep: true
    }
  }
};
</script>
<style scoped>
.text-line {
  background-color: transparent;
  color: #fff;
  outline: none;
  outline-style: none;
  border-top: none;
  border-left: none;
  border-right: none;
  border-bottom: solid #fff 2px;
  padding: 3px 1px;
  width: 100%;
  margin-bottom: 40px;
}
input > ::placeholder {
  color: #fff;
}
#clickableAwesomeFont {
  cursor: pointer;
}
#favourite {
  color: #fff;
  font-size: 16px;
}
#tasks {
  color: #fff;
  font-size: 16px;
}
p {
  text-align: left;
  font-weight: 350;
  font-family: "Raleway", sans-serif;
}
h5 {
  text-align: left;
  font-size: 17px;
  justify-content: space-around;
}
.card {
  background-color: #fff;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  font-size: 20px;
  min-height: 50px;
  text-align: left;
}
</style>