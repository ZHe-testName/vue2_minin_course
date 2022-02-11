<template>
  <div>
    <h2>Todos</h2>

    <router-link to="/">go home</router-link>
    <hr>
    <!--v-bind для передачи данных в компоненты -->
    <AddTodoItem @add-todo="addTodo"/>

    <select v-model="filter">
        <option value="all">All</option>
        <option value="compleated">Compleated</option>
        <option value="not-compleated">Not compleated</option>
    </select>

    <!-- @ - заменяет v-on -->
    <!-- v-if используется для условного рендеринга
    компонент будет показан если условие true -->
    <Loader v-if="loading"/>
    <TodoList 
      v-bind:todos="filteredToDo"
      @remove-todo="removeTodo"
      v-else-if="filteredToDo.length"
    />
    <!-- иначе.... -->
    <p v-else>No todos!</p>
  </div>
</template>

<script>
//собака в названии пути указывает на папку src
//что ооочень удобно
import TodoList from '@/components/TodoList.vue';
import AddTodoItem from '@/components/AddTodoItem.vue';
import Loader from '@/views/Loader.vue';;

export default {
  name: 'App',
  //для обявсения переменных с данными
  data() {
    return {
      todos: [],
      loading: true,
      filter: 'all',
    };
  },
  //данное свойство используется для того чтоби следить
  //и реагитровать на изменения каких либо переменных
  //для этого нужно создать метод который будет называтся так как 
  //интересующее нас свойство
//   watch: {
//       filter(value){
//           console.log(value);
//       },
//   },

//в поле computed мы описываем функции которые
//зависят от каких то вю переменных и моделей
//функции из этого поля ведут себя можно сказать как переменные
computed: {
    filteredToDo(){
        switch(this.filter){
            case 'all':
                return this.todos;
            case 'compleated':
                return this.todos.filter(item => item.status);
            case 'not-compleated':
                return this.todos.filter(item => !item.status);
        };
    },
},

  //для добавления и регистрации компонент
  components: {
    TodoList,
    AddTodoItem,
    Loader,
  },
  //метод которы фызывается когда компонент полностю в монтирован в DOM
  mounted(){
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=5')
        .then(response => response.json())
        .then(json => {
            this.todos = json;
            this.loading = false;
        })
  },
  methods: {
    removeTodo(id){
      this.todos = this.todos.filter(item => item.id !== id);
    },
    addTodo(todo){
      this.todos.push(todo);
    }
  }
}
</script>