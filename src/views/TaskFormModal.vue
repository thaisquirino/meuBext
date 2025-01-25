<template>
  <div class="modal-overlay">
    <div class="modal-content">
      <h3 class="text-xl font-bold mb-4">Adicionar Tarefa</h3>
      <form @submit.prevent="saveTask">
        <input v-model="task.title" type="text" placeholder="Título" class="input mb-2" required />
        <textarea v-model="task.description" placeholder="Descrição" class="textarea mb-2"></textarea>
        <select v-model="task.priority" class="select mb-2">
          <option value="Baixa">Baixa</option>
          <option value="Média">Média</option>
          <option value="Alta">Alta</option>
        </select>
        <select v-model="task.category" class="select mb-2">
          <option value="Pessoal">Pessoal</option>
          <option value="Trabalho">Trabalho</option>
          <option value="Estudo">Estudo</option>
        </select>
        <input v-model="task.dueDate" type="date" class="input mb-4" />
        <button type="submit" class="btn-primary w-full">Salvar</button>
      </form>
      <button @click="$emit('close')" class="btn-secondary mt-2 w-full">Cancelar</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      task: {
        title: "",
        description: "",
        priority: "Baixa",
        category: "Pessoal",
        dueDate: "",
      },
    };
  },
  methods: {
    saveTask() {
      this.$emit("saveTask", { ...this.task });
      this.resetForm();
    },
    resetForm() {
      this.task = { title: "", description: "", priority: "Baixa", category: "Pessoal", dueDate: "" };
    },
  },
};
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  inset: 0;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}
.modal-content {
  background: white;
  padding: 20px;
  border-radius: 10px;
  max-width: 400px;
  width: 100%;
}
</style>
