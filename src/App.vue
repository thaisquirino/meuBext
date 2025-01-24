<template>
  <div id="app">
    <header>
      <h1>Bem-vindo à Aplicação de Tarefas</h1>
    </header>

    <!-- Roteamento Condicional ou Navegação -->
    <div>
      <Login v-if="!isAuthenticated" @login="handleLogin" />
      <Dashboard v-else />
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import Login from "./components/Login.vue"; // Componente de Login
import Dashboard from "./views/Dashboard.vue";  // Dashboard está em views/

export default {
  components: {
    Login,
    Dashboard,
  },
  setup() {
    const isAuthenticated = ref(false); // Controle de autenticação

    const handleLogin = () => {
      isAuthenticated.value = true;
    };

    return {
      isAuthenticated,
      handleLogin,
    };
  },
};
</script>

<style>
#app {
  text-align: center;
  padding: 20px;
}

header {
  background-color: #007bff;
  color: white;
  padding: 10px 0;
}

h1 {
  margin: 0;
}
</style>
