<template>
  <div class="dashboard-container">
    <div class="dashboard-content">
      <h2 class="dashboard-title">Dashboard</h2>
      <p class="dashboard-subtitle">Lista de tarefas</p>

      <div class="task-list">
        <ul>
          <li v-for="task in tasks" :key="task.id" class="task-item">
            <strong>{{ task.title }}</strong> - {{ task.priority }}
            <button class="task-button" @click="openTaskDetailsModal(task)">Detalhes</button>
            <button class="delete-button" @click="deleteTask(task.id)">Excluir</button>
          </li>
        </ul>
      </div>

      <button class="add-task-button" @click="openTaskFormModal">Adicionar Tarefa</button>
    </div>

    <!-- Modal para editar ou adicionar tarefa -->
    <TaskDetailsModal
      v-if="showTaskDetailsModal"
      :taskData="selectedTask"
      :isVisible="showTaskDetailsModal"
      @close="closeTaskDetailsModal"
      @save="saveTask"
    />
  </div>
</template>

<script>
import { ref } from "vue";
import TaskDetailsModal from "./TaskDetailsModal.vue";

export default {
  components: {
    TaskDetailsModal,
  },
  setup() {
    const tasks = ref([
      { id: 1, title: "Reunião Bext", priority: "Alta", description: "", dueDate: "" },
      { id: 2, title: "Fazer compras", priority:"Baixa", description: "", dueDate: "" },
      { id: 3, title: "Ir na academia", priority: "Alta", description: "", dueDate: "" },
    ]);
    const showTaskDetailsModal = ref(false);
    const selectedTask = ref(null);

    // Abre o modal para ver ou editar os detalhes da tarefa
    const openTaskDetailsModal = (task) => {
      selectedTask.value = { ...task }; // Cria uma cópia da tarefa para editar
      showTaskDetailsModal.value = true;
    };

    // Fecha o modal de detalhes
    const closeTaskDetailsModal = () => {
      showTaskDetailsModal.value = false;
    };

    // Função para salvar ou atualizar a tarefa
    const saveTask = (task) => {
      if (task.id) {
        // Se a tarefa já tem id, atualiza a tarefa existente
        const taskIndex = tasks.value.findIndex((t) => t.id === task.id);
        if (taskIndex !== -1) {
          tasks.value[taskIndex] = task; // Atualiza tarefa na lista
        }
      } else {
        // Se não tem id, é uma nova tarefa, então adiciona à lista
        task.id = Date.now(); // Atribui um ID único
        tasks.value.push(task); // Adiciona nova tarefa à lista
      }
      closeTaskDetailsModal(); // Fecha o modal após salvar
    };

    // Abre o modal para adicionar uma nova tarefa
    const openTaskFormModal = () => {
      selectedTask.value = { id: null, title: "", priority: "Média", description: "", dueDate: "" };
      showTaskDetailsModal.value = true;
    };

    // Função para excluir uma tarefa
    const deleteTask = (taskId) => {
      tasks.value = tasks.value.filter((task) => task.id !== taskId);
    };

    return {
      tasks,
      showTaskDetailsModal,
      selectedTask,
      openTaskDetailsModal,
      closeTaskDetailsModal,
      saveTask,
      openTaskFormModal,
      deleteTask, 
    };
  },
};
</script>

<style scoped>
.dashboard-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background-color: #000; 
  padding: 16px;
}

.dashboard-content {
  background-color: #e0e0e0;
  padding: 32px;
  border-radius: 12px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
  width: 100%;
  max-width: 800px;
  text-align: center;
}

.dashboard-title {
  color: #000;
  font-size: 32px;
  margin-bottom: 16px;
}

.dashboard-subtitle {
  color: #000;
  font-size: 18px;
  margin-bottom: 32px;
}

.task-list {
  margin-bottom: 32px;
}

.task-item {
  display: flex;
  justify-content: space-between; 
  align-items: center;
  background-color: #f5f5f5; 
  margin-bottom: 12px;
  padding: 12px;
  border-radius: 8px;
  overflow: hidden; 
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.task-item .task-content {
  display: flex;
  flex-direction: column;
  flex-grow: 1;
}

.task-item .task-content strong {
  font-size: 16px;
  margin-bottom: 6px;
}

.task-item button {
  margin-left: 10px;
  padding: 6px 12px;
  font-size: 14px;
  background-color: #007bff;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.task-item button:hover {
  background-color: #0056b3;
}

.delete-button {
  background-color: #f44336;
  color: white;
  border: none;
  padding: 6px 12px;
  border-radius: 4px;
  cursor: pointer;
}

.delete-button:hover {
  background-color: #d32f2f;
}

.add-task-button {
  padding: 12px 24px;
  background-color: #007bff;
  color: #fff;
  font-size: 16px;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.add-task-button:hover {
  background-color: #0056b3;
}

/* Responsividade */
@media (max-width: 768px) {
  .dashboard-content {
    padding: 24px;
  }

  .dashboard-title {
    font-size: 28px;
  }

  .dashboard-subtitle {
    font-size: 16px;
  }

  .task-item {
    flex-direction: column;
    align-items: flex-start;
  }

  .task-item button {
    margin-top: 8px;
    margin-left: 0;
    width: 100%; /* Botões ocupam 100% em telas menores */
    text-align: center;
  }

  .add-task-button {
    font-size: 14px;
    padding: 10px 20px;
  }
}
</style>