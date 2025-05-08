<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import TodoList from './components/TodoList.vue';


const estado = reactive({
  filtro: 'todas',
  tarefaTemp: '',
  tarefas: [
    {
      titulo: 'Estudar ES6',
      finalizada: false,
    },
    {
      titulo: 'Estudar SASS',
      finalizada: false,
    },
    {
      titulo: 'Estudar Node.js',
      finalizada: false,
    },
    {
      titulo: 'Estudar Express.js',
      finalizada: false,
    }
  ],
});

const getTarefasPendentes = () => { 
  return estado.tarefas.filter(tarefa => !tarefa.finalizada)
};

const getTarefasFinalizadas = () => { 
  return estado.tarefas.filter(tarefa => tarefa.finalizada)
};

const getTarefasFiltradas = () => {
  const { filtro } = estado;

  switch (filtro) {
    case 'pendentes':
      return getTarefasPendentes();
    case 'finalizadas':
      return getTarefasFinalizadas();
  
    default:
      return estado.tarefas;
      break;
  };
};

const cadastraTarefa = () => {
  const newTask = {
    titulo: estado.tarefaTemp,
    finalizada: false,
  };
  estado.tarefas.push(newTask);
  estado.tarefaTemp = '';
};

</script>

<template>
  <div class="container">
    <Cabecalho :tarefasPendentes="getTarefasPendentes().length" />
    <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastraTarefa" />
    <TodoList :tarefas="getTarefasFiltradas()" />
  </div>
</template>