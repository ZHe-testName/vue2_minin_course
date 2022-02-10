<template>
  <div>
    <ul>
        <!-- Для итерации по массивам нужно использоавать v-for -->
        <!-- И в v-bind можно передавать нужный нам елемент в итерируемую компоненту -->
      <TodoItem 
        v-for="(todo, index) of todos" :key="index"
        v-bind:todo="todo"
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
}
</script>
