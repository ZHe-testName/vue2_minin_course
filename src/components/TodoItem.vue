<template>
    <!-- при помощи интерполяции которая позволяет выводить динамически значения подставляем в элемент -->
    <li>
        <span>
            <input type="checkbox">
            <strong>{{todo.id}}</strong>
            {{todo.title}}
        </span>
        <button>&times;</button>
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
        }
    },
}
</script>