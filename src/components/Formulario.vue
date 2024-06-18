<script setup>
const props = defineProps(['cadastraTarefas', 'tarefaTemp', 'editaTarefaTemp', 'trocafilto'])
</script>
<template>
    <form @submit.prevent="props.cadastraTarefas">
        <div class="row">
            <div class="col">
                <input :value="props.tarefaTemp" @change="props.editaTarefaTemp"
                    type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control">
            </div>
            <div class="col-md-2">
                <button type="submit" class="btn btn-primary">cadastrar</button>
            </div>
            <div class="col-md-2">
                <select class="form-control" @change="props.trocafilto">
                    <option value="todas">Todas tarefas</option>
                    <option value="pendentes">Pendentes</option>
                    <option value="finalizadas">Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>