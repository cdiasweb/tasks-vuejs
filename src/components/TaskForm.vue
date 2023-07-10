<template>
  <div class="overlay" @click.self="$emit('close')">
    <div class="task-form-container">
      <h3>Adicionar tarefa</h3>
      <span v-if="errorMessage" class="error">
        <b>Erro:</b> {{errorMessage}}
      </span>
      <div class="task-form">
        <label for="taskName">Nome</label>
        <input id="taskName" type="text" v-model="task.name"/>

        <label for="taskDescription">Descrição</label>
        <input type="text" id="taskDescription" v-model="task.description"/>

        <label for="taskStatus">Status</label>
        <select id="taskStatus" type="text" v-model="task.status">
          <option v-for="(status, index) in taskStatuses" :key="index" :value="status.value">
            {{ status.label }}
          </option>
        </select>

        <div class="controls-container">
          <div class="controls">
            <button class="save-button" @click="handleSave">Save</button>
            <button v-if="task.hasOwnProperty('id')" class="delete-button" @click="$emit('delete')">Delete</button>
            <button class="close-button" @click.self="$emit('close')">Fechar</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TaskForm',
  props: {
    selectedTask: { type: Object, default: () => { return {} } }
  },
  watch: {
    selectedTask (newValue) {
      this.task = newValue
    }
  },
  data () {
    return {
      task: {
        name: '',
        description: '',
        status: 'pending'
      },
      taskStatuses: [
        {
          label: 'Pendente',
          value: 'pending'
        },
        {
          label: 'Concluída',
          value: 'done'
        }
      ],
      errorMessage: ''
    }
  },
  methods: {
    valid () {
      return this.task.description && this.task.name && this.task.status
    },
    handleSave () {
      if (this.valid()) {
        this.errorMessage = ''
        this.$emit('save', this.task)
      } else {
        this.errorMessage = 'Informe o nome, descrição e status para a tarefa.'
      }
    }
  }
}
</script>

<style scoped>
.overlay {
  position: absolute;
  left: 0px;
  top: 0px;
  width: 100%;
  height: 100%;
  background-color: rgba(0,0,0,0.69);
  display: flex;
  align-items: center;
}

.task-form-container {
  width: 400px;
  margin: 0 auto;
  background-color: white;
  border-radius: 5px;
  border: solid 1px white;
  padding: 5px;
}

.task-form {
  display: flex;
  flex-direction: column;
  text-align: left;
}

.controls {
  display: flex;
  padding: 5px;
}

.controls-container {
  display: flex;
  justify-content: end;
}

.save-button {
  background-color: rgba(29,49,255,0.69);
  color: white;
}

.delete-button {
  background-color: rgba(255,8,0,0.69);
  color: white;
}

.close-button {
  background-color: #2c3e50;
  color: white;
}

.error {
  background-color: #c94d4d;
  color: white;
  padding: 4px;
  border-radius: 4px;
  font-size: 12px;
}
</style>
