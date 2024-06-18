<script setup>
const props = defineProps(['tarefa'])
</script>
<template>
    <ul class="list-group mt-4" v-if="props.tarefa.length > 0 ">
        
        <li class="list-group-item" v-for="tarefa in props.tarefa">

            <input @change="evento => tarefa.Finalizada = evento.target.checked" :checked="tarefa.Finalizada"
                :id="tarefa.titulo" type="checkbox">
            <label :class="{ done: tarefa.Finalizada }" class="ms-3" :for="tarefa.titulo">
                {{ tarefa.titulo }}
            </label>
        </li>
        </ul>
        <span v-else>Não a tarefas</span>
</template>

<style scoped>
.done {
    text-decoration: line-through;
}
</style>
