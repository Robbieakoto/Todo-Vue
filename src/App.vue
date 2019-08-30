<template>
  <div id="app">
    <AddTask />
  </div>
</template>

<script>
import AddTask from "./components/AddTask";
import Favourite from "./components/Favorite";
import TasksList from "./components/TasksList";

export default {
  name: "app",
  components: {
    AddTask,
    Favourite,
    TasksList
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
