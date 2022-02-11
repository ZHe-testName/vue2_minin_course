<template>
<!-- .prevent - используется для отмены стандартного поведения формы
чтобы страничка не перезагружалась -->
    <form @submit.prevent="onSubmit">
        <!-- чтобы связать value инпута с скриптом используется директива v-model
        к которой мы привязываем нужные переменные с данными -->
        <input type="text" v-model="title">
        <button>Create</button>
    </form>
</template>

<script>
export default {
    data (){
        return {
            title: ''
        };
    },
    methods: {
        onSubmit (){
            if(this.title.trim()){
                const newTodo = {
                    id: Date.now(),
                    title: this.title,
                    status: false,
                };

                this.$emit('add-todo', newTodo);
                this.title = '';
            }
        },
    },
}
</script>

<style scoped>
    form{
        display: flex;
        margin-bottom: 20px;
    }

    input{
        width: 400px;
        margin-right: 15px;
    }
</style>