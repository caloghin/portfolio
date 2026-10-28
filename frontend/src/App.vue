<script setup>
import { onMounted, ref } from 'vue'

const health = ref(null)
const error = ref('')

onMounted(async () => {
  try {
    const response = await fetch('/api/hello')

    if (!response.ok) {
      throw new Error(`HTTP ${response.status}`)
    }

    health.value = await response.json()
  } catch (err) {
    error.value =
      'Could not connect to the backend. Make sure Spring Boot is running.'
  }
})
</script>

<template>
  <main class="page">
    <section class="hero">
      <p class="eyebrow">FULL-STACK DEVELOPER PORTFOLIO</p>
      <h1>My Portfolio Project</h1>
      <p class="subtitle">
        Built with Vue 3, Spring Boot, PostgreSQL and Gradle.
      </p>

      <div class="status">
        <p v-if="health">
          Backend status:
          <strong>{{ health.status }}</strong>
        </p>

        <p v-else-if="error" class="error">
          {{ error }}
        </p>

        <p v-else>Checking backend connection...</p>
      </div>
    </section>
  </main>
</template>

<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: Inter, system-ui, sans-serif;
  background: #0b1020;
  color: #f5f7ff;
}

.page {
  min-height: 100vh;
  display: grid;
  place-items: center;
  padding: 24px;
}

.hero {
  width: min(100%, 760px);
  padding: 48px;
  border: 1px solid #29334b;
  border-radius: 24px;
  background: #121a2d;
}

.eyebrow {
  color: #8ca9ff;
  font-size: 0.8rem;
  letter-spacing: 0.15em;
  font-weight: 700;
}

h1 {
  font-size: clamp(2rem, 6vw, 4rem);
  margin-bottom: 16px;
}

.subtitle {
  color: #bac5dc;
  line-height: 1.7;
}

.status {
  margin-top: 32px;
  padding: 16px;
  border-radius: 12px;
  background: #1b2740;
}

.error {
  color: #ff9e9e;
}
</style>
