<script setup>
import { reactive } from 'vue';

const estado = reactive({
  filtro: 'todas',
  tarefaTemp: '',
  tarefas: [
    {
      titulo: 'Estudar ES6',
      Finalizada: false
    },
    {
      titulo: 'Estudar Sass',
      Finalizada: false
    },
    {
      titulo: 'Ir á academía',
      Finalizada: true
    }
  ]

})

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.Finalizada === true)
  }
    const getTarefasPendentes = () => {
      return estado.tarefas.filter(tarefa => tarefa.Finalizada === false)
    }

const getTarefasfiltradas = () => {
  const { filtro } = estado;

  switch(filtro){
    case 'pendentes':
      return getTarefasPendentes();
      case 'finalizadas':
        return getTarefasFinalizadas();
        default:
          return estado.tarefas;
      
  }
}

const cadastraTarefas = () =>{
  const tarefaNova = {
    titulo: estado.tarefaTemp,
    Finalizada :false
  }
  estado.tarefas.push(tarefaNova);
  estado.tarefaTemp= '';
}


</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4  bg-light rounded-3">
      <h1>Minhas Tarefas</h1>
      <p>Você possui {{ getTarefasPendentes().length }} tarefas pendentes</p>
    </header>

    <form @submit.prevent="cadastraTarefas"> 
      <div class="row">
        <div class="col">
          <input :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control">
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">cadastrar</button>
        </div>
        <div class="col-md-2">
          <select class="form-control" @change="evento => estado.filtro = evento.target.value">
            <option value="todas">Todas tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefasfiltradas()">
        <input @change="evento => tarefa.Finalizada = evento.target.checked" :checked="tarefa.Finalizada" :id="tarefa.titulo" type="checkbox">
        <label :class="{ done: tarefa.Finalizada }" class="ms-3" :for="tarefa.titulo">
          {{ tarefa.titulo }}
        </label>
      </li>
    </ul>
  </div>


</template>
<style scoped>
.done {
  text-decoration: line-through;
}
</style>
