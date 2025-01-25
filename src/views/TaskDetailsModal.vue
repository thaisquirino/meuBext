<template>
  <div v-if="isVisible" class="modal-overlay">
    <div class="modal-content">
      <h3 class="modal-title">Detalhes da Tarefa</h3>
      <form @submit.prevent="saveTask">
        <div class="form-group">
          <label for="title">Título:</label>
          <input
            type="text"
            id="title"
            v-model="task.title"
            placeholder="Título da Tarefa"
            required
          />
        </div>

        <div class="form-group">
          <label for="description">Descrição:</label>
          <textarea
            id="description"
            v-model="task.description"
            placeholder="Descrição da Tarefa"
          ></textarea>
        </div>

        <div class="form-row">
          <div class="form-group priority-group">
            <label for="priority">Prioridade:</label>
            <select v-model="task.priority" id="priority">
              <option value="Baixa">Baixa</option>
              <option value="Média">Média</option>
              <option value="Alta">Alta</option>
            </select>
          </div>

          <div class="form-group date-group">
            <label for="dueDate">Data de Conclusão:</label>
            <input type="date" id="dueDate" v-model="task.dueDate" />
          </div>
        </div>

        <div class="modal-actions">
          <button type="button" @click="closeModal">Fechar</button>
          <button type="submit">Salvar</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    taskData: Object,
    isVisible: Boolean,
  },
  data() {
    return {
      task: { ...this.taskData }, // Faz uma cópia do objeto recebido
    };
  },
  methods: {
    saveTask() {
      this.$emit("save", this.task);
      this.closeModal();
    },
    closeModal() {
      this.$emit("close");
    },
  },
};
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.6);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-content {
  background-color: #1a1a1a;
  padding: 32px;
  border-radius: 12px;
  width: 100%;
  max-width: 500px;
  color: #fff;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
}

.modal-title {
  font-size: 24px;
  margin-bottom: 16px;
  color: #fff;
  text-align: center; 
}

.form-group {
  margin-bottom: 16px;
}

.form-group label {
  display: block;
  color: #fff;
  margin-bottom: 8px;
}

.form-group input,
.form-group textarea,
.form-group select {
  width: 100%; 
  padding: 12px;
  border-radius: 8px;
  border: 1px solid #333;
  background-color: #262626;
  color: #fff;
  box-sizing: border-box; 
}

.form-group textarea {
  resize: vertical;
}

.form-group input[type="date"] {
  width: 100%;
  max-width: 100%;
  padding: 12px;
  border-radius: 8px;
  border: 1px solid #333;
  background-color: #262626;
  color: #fff;
  box-sizing: border-box;
}

.modal-actions {
  display: flex;
  justify-content: center;
  gap: 16px; 
  margin-top: 20px;
}

.modal-actions button {
  padding: 10px 20px;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.modal-actions button[type="button"] {
  background-color: #ff4d4d;
  color: #fff;
}

.modal-actions button[type="submit"] {
  background-color: #007bff;
  color: #fff;
}

.modal-actions button:hover {
  background-color: #0056b3;
}

@media (max-width: 768px) {
  .form-group {
    display: flex;
    flex-direction: column;
    align-items: flex-start; 
  }

  .form-group input[type="date"] {
    width: 100%; /* Ajusta a largura para telas menores */
  }
}

</style>