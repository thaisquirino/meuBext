<template>
  <div class="login-container">
    <form class="login-form" @submit.prevent="handleLogin">
      <h1>Login</h1>
      <div>
        <input
          type="text"
          v-model="username"
          placeholder="Usuário"
          required
        />
      </div>
      <div>
        <input
          type="password"
          v-model="password"
          placeholder="Senha"
          required
        />
      </div>
      <div v-if="errorMessage" class="error-message">
        {{ errorMessage }}
      </div>
      <button type="submit">Entrar</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      username: "", // Armazena o nome de usuário digitado
      password: "", // Armazena a senha digitada
      errorMessage: "", // Exibe mensagens de erro
    };
  },
  methods: {
    handleLogin() {
    if (this.username === "admin" && this.password === "1234") {
      this.$router.push('/dashboard'); // Direciona para a página de dashboard após login bem-sucedido
    } else {
      this.errorMessage = "Usuário ou senha incorretos.";
    }
  },
}
};
</script>
<style scoped>
/* Estilo do container principal */
.login-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh; /* Ocupa a altura total da tela */
  background-color: #000; /* Fundo preto */
  padding: 16px; /* Espaçamento interno para telas menores */
}

/* Estilo do formulário */
.login-form {
  background-color: #1a1a1a; /* Fundo cinza escuro */
  padding: 32px;
  border-radius: 12px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
  width: 100%;
  max-width: 400px;
  text-align: center;
  display: flex;
  flex-direction: column; /* Garante que os elementos sejam alinhados na vertical */
  gap: 16px; /* Espaçamento entre os elementos */
}

/* Título do formulário */
.login-form h1 {
  color: #fff;
  margin-bottom: 24px;
  font-size: 24px;
}

/* Inputs */
.login-form input {
  width: 100%;
  padding: 12px;
  margin-bottom: 16px;
  border: 1px solid #333;
  border-radius: 8px;
  background-color: #262626;
  color: #fff;
  font-size: 16px;
  box-sizing: border-box; /* Garante que o padding não aumente o tamanho do input */
}

/* Placeholder */
.login-form input::placeholder {
  color: #aaa;
}

/* Botão */
.login-form button {
  width: 100%;
  padding: 12px;
  background-color: #007bff; /* Azul forte */
  color: #fff;
  font-size: 16px;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.login-form button:hover {
  background-color: #0056b3; /* Azul mais escuro ao passar o mouse */
}

/* Mensagem de erro */
.error-message {
  color: #ff4d4d; /* Vermelho para mensagens de erro */
  margin-bottom: 16px;
  font-size: 14px;
  text-align: center;
}

/* Responsividade: ajusta o layout em telas menores */
@media (max-width: 480px) {
  .login-form {
    padding: 24px; /* Reduz o padding para telas pequenas */
  }
  
  .login-form input {
    font-size: 14px; /* Reduz o tamanho da fonte dos inputs em telas menores */
  }

  .login-form button {
    font-size: 14px; /* Reduz o tamanho da fonte do botão */
  }
}
</style>

