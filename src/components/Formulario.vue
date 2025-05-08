<script setup>
    const props = defineProps(['cadastraTarefa', 'tarefaTemp', 'trocarFiltro', 'editaTarefaTemp'])
</script>

<template>
    <form @submit.prevent="cadastraTarefa">
    <div class="row">
    <div class="col">
        <input :value="tarefaTemp" @change="editaTarefaTemp" required class="form-control" type="text" placeholder="Digite aqui a descrição da tarefa">
    </div>
    <div class="col-md-2">
        <button type="submit" class="btn btn-primary">Cadastrar</button>
    </div>
    <div class="col-md-2">
        <select @change="trocarFiltro" class="form-control">
        <option value="todas">Todas as tarefas</option>
        <option value="pendentes">Pendentes</option>
        <option value="finalizadas">Finalizadas</option>
        </select>
    </div>
    </div>
</form>
</template>