<template>
  <div class="login-container">
    <div class="card">
        <div @click="navigateToHome()" class="back-btn">
        <ChevronLeft/>
          <p>Vissza</p>
        </div>
      <div class="header">
        <img src="../assets/logo.svg" alt="Vasvári App Logo" class="logo">
        <h1>Bejelentkezés</h1>
      </div>

      <form @submit.prevent="handleSubmit" class="form">
        <div class="input-group">
          <div class="input-wrapper">
          <label for="email">Email cím</label>
            <input
                type="email"
                id="email"
                v-model="email"
                placeholder="pelda@vasvari.com"
                required
                :class="{ 'invalid': emailError }"
                @input="validateEmail"
            >
            <div class="input-icon">
              <Mail/>
            </div>
          </div>
          <div class="error-message" v-if="emailError">
            <span class="error-icon">!</span>
            {{ emailError }}
          </div>
        </div>

        <div class="input-group">
          <div class="input-wrapper">
          <label for="password">Jelszó</label>
            <input
                type="password"
                id="password"
                v-model="password"
                placeholder="••••••••"
                required
                :class="{ 'invalid': passwordError }"
                @input="validatePassword"
            >
            <div class="input-icon">
              <Lock/>
            </div>
          </div>
          <div class="error-message" v-if="passwordError">
            <span class="error-icon">!</span>
            {{ passwordError }}
          </div>
        </div>

        <button type="submit" class="submit-btn" :disabled="loading">
          <span v-if="!loading">Bejelentkezés</span>
          <div v-else class="loader"></div>
        </button>

        <div class="links">
          <a href="#" class="forgot-password">Elfelejtetted a jelszavad?</a>
        </div>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { Mail, Lock,ChevronLeft } from 'lucide-vue-next';
import { useRouter } from 'vue-router';

const router = useRouter();

const navigateToHome = () => {
  router.push('/');
};


const email = ref('');
const password = ref('');
const emailError = ref('');
const passwordError = ref('');
const loading = ref(false);

const validateEmail = () => {
  const re = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  if (!re.test(email.value)) {
    emailError.value = 'Érvénytelen email cím';
  } else {
    emailError.value = '';
  }
};

const validatePassword = () => {
  if (password.value.length < 6) {
    passwordError.value = 'A jelszónak legalább 6 karakter hosszúnak kell lennie';
  } else {
    passwordError.value = '';
  }
};

const handleSubmit = async () => {
  validateEmail();
  validatePassword();

  if (!emailError.value && !passwordError.value) {
    loading.value = true;
    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 1500));
    loading.value = false;
    // Handle actual login logic here
  }
};
</script>

<style scoped>
.login-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background: linear-gradient(135deg, #4a1d6b, #8a4baf);
  padding: 2rem;
}
.back-btn{
  color: mediumpurple;
  display: flex;
  flex-direction: row;
  width: fit-content;
  cursor: pointer;
}

.card {
  background: rgba(255, 255, 255, 0.95);
  padding: 2.5rem;
  border-radius: 20px;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
  width: 100%;
  max-width: 450px;
  transition: transform 0.3s ease;
}

.card:hover {
  transform: translateY(-5px);
}

.header {
  text-align: center;
  margin-bottom: 2rem;
}

.logo {
  height: 60px;
  margin-bottom: 1.5rem;
}

h1 {
  color: #2d3748;
  font-size: 1.8rem;
  margin-bottom: 0.5rem;
}

.input-group {
  margin-bottom: 1.5rem;
  width: 100%;
}

label {
  display: block;
  color: #4a5568;
  font-weight: 500;
  margin-bottom: 0.5rem;
}

.input-wrapper {
  width: 100%;
  position: relative;
}

input {
  width: 100%;
  padding: 0.875rem 1rem 0.875rem 2.5rem;
  border: 2px solid #e2e8f0;
  border-radius: 8px;
  font-size: 1rem;
  transition: border-color 0.3s ease;
}

input:focus {
  outline: none;
  border-color: #667eea;
  box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
}

.input-icon {
  color: rgba(0, 0, 0, 0.3);
  position: absolute;
  top: 4.9vh;
  left: 0.65vw;
}

input.invalid {
  border-color: #fc8181;
}

.error-message {
  color: #fc8181;
  font-size: 0.875rem;
  margin-top: 0.5rem;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.error-icon {
  background: #fc8181;
  color: white;
  width: 18px;
  height: 18px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
  font-size: 0.75rem;
}

.submit-btn {
  width: 100%;
  padding: 1rem;
  background: linear-gradient(45deg, #8746ef, #6b2ee3);
  color: white;
  border: none;
  border-radius: 8px;
  font-weight: 600;
  cursor: pointer;
  transition: transform 0.2s ease, opacity 0.2s ease;
  margin-top: 1rem;
}

.submit-btn:hover:not(:disabled) {
  transform: scale(1.02);
  opacity: 0.95;
}

.submit-btn:disabled {
  opacity: 0.7;
  cursor: not-allowed;
}

.loader {
  border: 3px solid #f3f3f3;
  border-top: 3px solid #667eea;
  border-radius: 50%;
  width: 24px;
  height: 24px;
  animation: spin 1s linear infinite;
  margin: 0 auto;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

.links {
  margin-top: 1.5rem;
  text-align: center;
}

.forgot-password {
  color: #667eea;
  text-decoration: none;
  font-size: 0.875rem;
  transition: color 0.2s ease;
}

.forgot-password:hover {
  color: #764ba2;
}

@media (max-width: 480px) {
  .card {
    padding: 1.5rem;
  }

  h1 {
    font-size: 1.5rem;
  }
}
</style>