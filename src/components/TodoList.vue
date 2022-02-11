<template>
  <div>
    <ul>
        <!-- Для итерации по массивам нужно использоавать v-for -->
        <!-- И в v-bind можно передавать нужный нам елемент в итерируемую компоненту -->

        <!-- чтобы связать дочернюю компоненту с родительской
        в родительской компоненте в диррективу v-on: после двоеточия 
        нужно написать название собития которое мы придумали -->
      <TodoItem 
        v-for="(todo, index) of todos" :key="index"
        v-bind:todo="todo"
        v-bind:index="index"
        v-on:remove-todo="removeTodo"
        />
    </ul>
  </div>
</template>

<script>
import TodoItem from '@/components/TodoItem.vue'

export default {
  //для того чтобы компонента знала что мы в нее передаем
  //используется свойство props
  //в масиве которого и прописываются названия переменных с нужными данными
  props: ['todos'],
  components: {
    TodoItem,
  },
  //для определения методов компоненты
  methods: {
    //ТУТ МОЖНО ОБРАТИТСЯ тоже к родительской компоненте чтобы передать данные
    removeTodo(id){
      this.$emit('remove-todo', id);
    },
  },
}
</script>

<style scoped>
/* ДЛя стилей

scoped используется для того чтобы стили были видны только для этой компоненты */
ul{
  list-style-type: none;
  margin: 0px;
  padding: 0px;
}

</style>