<template>
    <header>
        <h1>{{ title }}</h1>
        <ButtonVue @btn-click="$emit('show-add-task')" 
        :text=" showAddTask ? 'Fechar' : 'Adicionar Tarefa' " 
        :color=" showAddTask ? 'red' : '#3fd3f8' " />
    </header>
</template>

<script>
import ButtonVue from './Button.vue'

    export default{
        name: "Header",
        props: {
            title: String,
            showAddTask: Boolean
        },
        components: {
            ButtonVue,
        }
    }
</script>

<!--"scoped" para os estilos serem apenas para esse componente-->

<style scoped>
    header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 20px;
    }

    h1 {
        font-size: 30px;
        font-weight: 500;
        color: white;
    }
</style>