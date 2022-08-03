<script setup>
import AppHeader from './components/AppHeader.vue'
import AppContent from './components/AppContent.vue'
</script>

<template>
  <header class="wrapper-out sticky top-0 z-100">
    <div class="wrapper">
      <AppHeader />
    </div>
  </header>

  <main class="wrapper">
    <div class="main">
      <AppContent
        v-for="(item, idx) in 5"
        :key="idx"
      />
    </div>
  </main>
</template>

<style lang="scss">
@import './assets/base.css';

#app {
  position: relative;
  min-width: 100%;
  min-height: 100vh;
  margin: 0 auto;
  font-weight: normal;
}

.router-link-exact-active {
  color: var(--color-text);
}

.router-link-exact-active:hover {
  background-color: transparent;
}

.wrapper-out {
  margin: 0 auto;
  background: var(--vt-c-white);
}

.wrapper {
  max-width: 1280px;
  margin: 0 auto;
}
</style>
