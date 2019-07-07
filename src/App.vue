<template>
  <div id="app">
    <TodoList/>
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue'

export default {
  name: 'app',
  components: {
    TodoList
  }
}
</script>

<style>
html{
  height: 100%;
}
body{
  background: #e3e3e3;
}
#app {
  font-family: "Open Sans", 'Noto Sans HK', sans-serif;
  min-width: 230px;
  max-width: 550px;
  margin: 0 auto;
}
</style>
