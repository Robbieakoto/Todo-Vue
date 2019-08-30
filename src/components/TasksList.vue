<template>
  <div class="Tasks" style="margin-top:10px;">
    <div class="row">
      <div class="col-1 col-md-1 col-lg-2"></div>

      <div class="col-10 col-md-9 col-lg-7">
        <div id="tasks">
          <p>
            <b>Tasks</b>
          </p>
        </div>

        <div
          class="card bg-light"
          style="margin-bottom:10px;"
          v-for="todo in todos"
          v-if="!todo.favourite"
          :key="todo.id"
        >
          <div class="row" style="padding:8px;">
            <div class="col-8 col-md-10 col-lg-10">
              <span style="float:left;">{{ todo.title }}</span>
            </div>
            <div class="col-4 offset-0 col-md-2 offset-md-0 col-lg-2 offset-lg-0">
              <i class="fa fa-star-o" style></i>&nbsp;&nbsp;&nbsp;
              <i class="fa fa-trash" style="color:#4C4C4C"></i>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "TasksList",
  data: function() {
    return {
      todos: todoStorage.fetch()
    };
  },
  methods: {
    removeTodo: function(todo) {
      this.todos.splice(this.todos.indexOf(todo), 1);
    }
  }
};
</script>

<style scoped>
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

