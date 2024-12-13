<template>
  <div class="grid-layout">
    <div class="left-grid">
      <h1>Planna</h1>
      <p>TO DO LIST para administrar tus tareas</p>
      <TaskInput @add-task="addTask" />
      <p class="warning-note">
        Las tareas se eliminan al refrescar la página. Esta es una versión beta, por lo que pueden
        ocurrir errores. Sitio pendiente a nuevas actualizaciones
      </p>
    </div>
    <div class="right-grid">
      <h2 class="task-title">Tareas</h2>
      <AddTask :tasks="tasks" />
    </div>
  </div>
</template>

<script>
import TaskInput from './TaskInput.vue'
import AddTask from './AddTask.vue'

export default {
  name: 'GridLayout',
  components: {
    TaskInput,
    AddTask,
  },
  data() {
    return {
      tasks: [],
    }
  },
  methods: {
    addTask(task) {
      this.tasks.push(task)
    },
  },
}
</script>

<style src="./GridLayout.css"></style>
