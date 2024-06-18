<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';

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

  switch (filtro) {
    case 'pendentes':
      return getTarefasPendentes();
    case 'finalizadas':
      return getTarefasFinalizadas();
    default:
      return estado.tarefas;

  }
}

const cadastraTarefas = () => {
  const tarefaNova = {
    titulo: estado.tarefaTemp,
    Finalizada: false
  }
  estado.tarefas.push(tarefaNova);
  estado.tarefaTemp = '';
}


</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
    <Formulario :trocafilto="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefas="cadastraTarefas"/>
      <ListaDeTarefas :tarefa="getTarefasfiltradas()"/>
  </div>


</template>


