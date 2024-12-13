<template>
  <div class="task-input-container">
    <input
      v-model="task"
      type="text"
      placeholder="Ingresa una tarea..."
      class="task-input"
      maxlength="50"
    />
    <button @click="handleAddTask" class="add-task-btn">
      <span>+</span> Agregar tarea
    </button>
  </div>
</template>

<script>
export default {
  name: 'TaskInput',
  data() {
    return {
      task: ''
    };
  },
  methods: {
    handleAddTask() {
      if (this.task.trim() !== '') {
        this.$emit('add-task', this.task);
        this.task = '';
      }
    }
  }
}
</script>

<style src="./TaskInput.css" scoped></style>
