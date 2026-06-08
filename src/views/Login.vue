<template>
  <div class="login">
    <a-card title="Login" style="width: 400px">
      <a-input
        v-model:value="username"
        placeholder="Username"
        style="margin-bottom: 16px"
      />

      <a-input-password
        v-model:value="password"
        placeholder="Password"
        style="margin-bottom: 16px"
      />

      <a-button type="primary" block @click="handleLogin">
        Login
      </a-button>
    </a-card>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()

const username = ref('')
const password = ref('')

const handleLogin = () => {
  const role = username.value === 'admin' ? 'admin' : 'user'

  localStorage.setItem('role', role)

  router.push('/dashboard')
}
</script>

<style scoped>
.login {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>