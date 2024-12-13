<template>
  <div>
    <ul class="task-list" v-if="tasks.length > 0">
      <transition-group name="task" tag="ul">
        <li v-for="(task, index) in tasks" :key="index" class="task-item">
          <span>{{ task }}</span>
          <font-awesome-icon
            :icon="['fas', 'trash']"
            @click="openDeleteModal(index)"
            class="delete-icon"
          />
        </li>
      </transition-group>
    </ul>
    <div v-else class="no-tasks">
      <img
        src="https://icons.veryicon.com/png/o/commerce-shopping/basic-icon-of-e-commerce/empty-21.png"
        alt="Empty box"
      />
      <p>Aún no hay tareas. ¿Qué tal si pruebas agregar una tarea?</p>
    </div>

    <ConfirmModal
      :isVisible="isModalVisible"
      :onConfirm="confirmDelete"
      :onCancel="cancelDelete"
    />
  </div>
</template>

<script>
import ConfirmModal from './ConfirmModal.vue';

export default {
  name: 'AddTask',
  components: {
    ConfirmModal
  },
  props: {
    tasks: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      isModalVisible: false,
      taskToDelete: null,
      dontShowModal: localStorage.getItem('dontShowDeleteModal') === 'true'
    };
  },
  methods: {
    openDeleteModal(index) {
      if (!this.dontShowModal) {
        this.isModalVisible = true;
        this.taskToDelete = index;
      } else {
        this.deleteTask(index);
      }
    },
    confirmDelete(dontShowAgain) {
      if (dontShowAgain) {
        this.dontShowModal = true;
        localStorage.setItem('dontShowDeleteModal', 'true');
      }
      this.deleteTask(this.taskToDelete);
      this.isModalVisible = false;
    },
    cancelDelete() {
      this.isModalVisible = false;
      this.taskToDelete = null;
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    }
  }
};
</script>

<style src="./AddTask.css"></style>
