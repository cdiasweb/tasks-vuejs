<template>
  <div>
    <h2>Tarefas Vue.js 2</h2>
    <task-form
      v-show="showTaskForm"
      :selected-task="selectedTask"
      @save="handleSaveTask"
      @close="showTaskForm = false"
      @delete="deleteTask"
    />
    <task-list
      :tasks="tasks"
      @showTaskForm="handleShowTaskForm"
    />
    <tasks-counter v-if="tasks.length > 0"/>
  </div>
</template>

<script>
import TaskList from '../components/TaskList'
import TaskForm from '../components/TaskForm'
import TasksCounter from '../components/TasksCounter'
export default {
  name: 'Home',
  components: { TasksCounter, TaskForm, TaskList },
  data () {
    return {
      tasks: [],
      showTaskForm: false,
      selectedTask: {}
    }
  },
  mounted () {
    let storageTasks = window.localStorage.getItem('tasks')
    if (storageTasks) {
      this.tasks = JSON.parse(storageTasks)
    }
  },
  methods: {
    updateLocalStorage () {
      window.localStorage.setItem('tasks', JSON.stringify(this.tasks))
    },
    handleSaveTask (task) {
      if (!task.hasOwnProperty('id')) {
        this.tasks.push(task)
      }

      this.updateLocalStorage()
      this.showTaskForm = false
      this.selectedTask = {}
    },
    handleShowTaskForm (task) {
      if (task) {
        task.id = this.tasks.indexOf(task)
      }
      if (task) {
        this.selectedTask = task
      }
      this.showTaskForm = true
    },
    deleteTask (id) {
      this.tasks.splice(id, 1)
      this.showTaskForm = false
      this.updateLocalStorage()
    }
  }
}
</script>

<style scoped>

</style>
