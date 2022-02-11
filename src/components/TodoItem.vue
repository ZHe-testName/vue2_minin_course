<template>
    <!-- при помощи интерполяции которая позволяет выводить динамически значения подставляем в элемент -->
    <!-- в директиве v-bind можно добавлять динамики html эллементам
    в свойство class нужно присвоить объект с отсдеживаемым свойством -->

    <!-- для навешивания слушателей собитий в vue
    тоже есть специальная директива v-on:[собитие] -->

    <!-- для того чтобы связать клик по кнопке удаления
    и данные в родительском компоненте используй метод $emit() 
    в него мы передаем название собития и данные -->
    <li>
        <span v-bind:class="{done: todo.status}">
            <input type="checkbox" v-on:change="todo.status = !todo.status">
            <strong>{{index + 1}}</strong>
            <!-- связываем значение и определенный фильтр -->
            {{todo.title | upperCase}}
        </span>
        <button class="rmButton" v-on:click="$emit('remove-todo', todo.id)">&times;</button>
    </li>
</template>

<script>
export default {
    //входные пропсы можно валидировать при помощи
    //объекта которй принимает соответствующие параметры
    //для валидации
    props: {
        todo: {
            //свойство должно быть объектом
            type: Object,
            //и оно обязательно
            required: true,
        },
        index: Number,
    },
    //фильтры нужны для преобразования данных в нутри шаблона
    filters: {
        upperCase (value){
            return value.toUpperCase();
        },
    },
}
</script>

<style scoped>
li{
    display: flex;
    justify-content: space-between;
    border: 1px solid black;
    padding: 0.5rem 2rem;
    margin-top: 1rem;
}

.rmButton{
    border-radius: 50%;
    background-color: tomato;
    font-weight: bold;
    color: #fff;
    border: 1px solid grey;
    cursor: pointer;
}

.done{
    text-decoration: line-through;
}

input{
    margin-right: 20px;
}
</style>