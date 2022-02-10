<template>
  <div id="app">
    <h1>Todo Application</h1>
    <!--v-bind для передачи данных в компоненты -->
    <TodoList 
      v-bind:todos="todos"
    />
  </div>
</template>

<script>
//собака в названии пути указывает на папку src
//что ооочень удобно
import TodoList from '@/components/TodoList.vue';
export default {
  name: 'App',
  //для обявсения переменных с данными
  data() {
    return {
      todos: [
        {id: 1, title: 'Buy the machinegun.', status: false},
        {id: 2, title: 'Buy 1000 bullets.', status: true},
        {id: 3, title: 'Buy the flower buket.', status: true}
      ],
    };
  },
  //для добавления и регистрации компонент
  components: {
    TodoList,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
