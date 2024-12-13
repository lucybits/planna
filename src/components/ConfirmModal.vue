<template>
  <div v-if="isVisible" class="modal-overlay">
    <div class="modal-content">
      <p>¿Estás seguro de que deseas eliminar esta tarea?</p>
      <label class="checkbox-label">
        <input type="checkbox" v-model="dontShowAgain" />
        No volver a preguntar
      </label>
      <div class="modal-actions">
        <button class="btn-cancel" @click="cancelDelete">Cancelar</button>
        <button class="btn-delete" @click="confirmDelete">Eliminar</button>
      </div>
    </div>
  </div>
</template>
  
<script>
export default {
  props: {
    isVisible: {
      type: Boolean,
      required: true
    },
    onConfirm: {
      type: Function,
      required: true
    },
    onCancel: {
      type: Function,
      required: true
    }
  },
  data() {
    return {
      dontShowAgain: false
    };
  },
  methods: {
    confirmDelete() {
      if (this.dontShowAgain) {
        localStorage.setItem('dontShowDeleteModal', 'true');
      }
      this.onConfirm(this.dontShowAgain);
    },
    cancelDelete() {
      this.onCancel();
    }
  }
};
</script>
  
<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(12, 16, 22, 0.8);
  display: flex;
  justify-content: center;
  align-items: center;
  backdrop-filter: blur(1px);
  animation: fadeIn 0.5s cubic-bezier(0.4, 0, 0.2, 1);
}
  
.modal-content {
  background: #131822;
  padding: 32px;
  border-radius: 16px;
  width: 380px;
  border: 1px solid rgba(255, 255, 255, 0.1);
  animation: slideUp 0.6s cubic-bezier(0.34, 1.56, 0.64, 1);
}
  
@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

@keyframes slideUp {
  from {
    opacity: 0;
    transform: translateY(40px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
  
.modal-content p {
  color: #FFFFFF;
  font-size: 18px;
  margin-bottom: 24px;
  font-weight: 500;
}
  
.checkbox-label {
  display: flex;
  align-items: center;
  gap: 8px;
  color: #8291A7;
  font-size: 14px;
}
  
input[type="checkbox"] {
  width: 20px;
  height: 20px;
  border-radius: 6px;
  border: 1px solid rgba(255, 255, 255, 0.2);
  appearance: none;
  background: #1F2835;
  cursor: pointer;
  position: relative;
}
  
input[type="checkbox"]:checked {
  background: #2A3545;
  border-color: #2A3545;
}

input[type="checkbox"]:checked::after {
  content: "✓";
  position: absolute;
  color: white;
  font-size: 14px;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
  
.modal-actions {
  margin-top: 32px;
  display: flex;
  justify-content: flex-end;
  gap: 12px;
}
  
button {
  padding: 12px 24px;
  border: none;
  font-size: 15px;
  font-weight: 500;
  cursor: pointer;
  border-radius: 10px;
  transition: all 0.2s ease;
}
  
.btn-delete {
  background: #dc3545;
  color: white;
}
  
.btn-cancel {
  background: #1F2835;
  color: white;
}
  
.btn-delete:hover {
  background: #bb2d3b;
}
  
.btn-cancel:hover {
  background: #161D27;
}
</style>