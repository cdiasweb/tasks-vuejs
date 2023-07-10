<template>
  <div class="content-container">
    <button @click="$emit('showTaskForm')" class="nova-tarefa">Nova tarefa</button>
    <div class="lista-tarefas" v-if="tasks.length > 0">
      <div class="tarefa" v-for="(task, index) in tasks" :key="index" @click="$emit('showTaskForm', task)">
        <div><b>{{ task.name }}</b></div>
        <div class="task-description">{{ task.description }}</div>
        <div class="task-status">{{ task.status }}</div>
      </div>
    </div>
    <div v-else>
      Parabéns, sem tarefas!
    </div>
  </div>
</template>

<script>
export default {
  name: 'TaskList',
  props: {
    tasks: { type: Array, default: () => {} }
  }
}
</script>

<style scoped>
.nova-tarefa {
  background-color: purple;
  color: white;
  margin: 10px;
}

.lista-tarefas {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.tarefa {
  border: solid 1px #6c176c;
  padding: 5px;
  border-radius: 5px;
  text-align: start;
  min-width: 400px;
  margin: 5px;
  font-size: 12px;
  cursor:pointer;
}

.tarefa:hover {
  background-color: #6c176c;
  color: white;
}

.task-status {
  float: right;
  font-size: 9px;
}
</style>
