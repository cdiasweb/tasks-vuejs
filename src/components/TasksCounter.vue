<template>
  <div>
    <div class='tasks-counter-container'>
      <span>Contador de tarefas</span><br>
      <div class="tasks-counter-list" v-for="(count,index) in counter" :key="index">
        <span>{{index}} {{count}} </span>
      </div>
    </div>
  </div>
</template>

<script setup>
import {computed, onMounted, ref} from 'vue'
const counter = ref({})
const updateCounter = () => {
  let tasks = localStorage.getItem('tasks')

  const statusTotals = {}

  if (tasks) {
    tasks = JSON.parse(tasks)
    tasks.forEach(item => {
      const status = item.status
      statusTotals[status] = (statusTotals[status] || 0) + 1
    })
  }

  counter.value = statusTotals
}

onMounted(() => {
  setInterval(() => {
    updateCounter()
  }, 500)
})
</script>

<style scoped>
.tasks-counter-container {
  color: purple;
}
.tasks-counter-list {
  font-size: 12px;
}
</style>
