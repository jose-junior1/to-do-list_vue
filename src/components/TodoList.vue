<script setup>
const props = defineProps({
    tarefas: {
        type: Array,
        required: true,
    }
});

function temTarefas() {
    if (props.tarefas.length <= 0) {
        return "Você não tem tarefas pendentes!";
    }
    return "";
}
</script>

<template>
    <ul class="list-group mt-4">
        <li class="list-group-item" v-if="temTarefas()">{{ temTarefas() }}</li>
        <li class="list-group-item" v-for="tarefa in tarefas" :key="tarefa.titulo">
            <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada"
                :id="tarefa.titulo" type="checkbox">
            <label :class="{ done: tarefa.finalizada === true }" class="ms-3" :for="tarefa.titulo">
                {{ tarefa.titulo }}
            </label>
        </li>
    </ul>
</template>

<style scoped>
.done {
    text-decoration: line-through;
}
</style>
