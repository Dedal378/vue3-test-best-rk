<script setup>
import IconRight from './icons/IconRight.vue'
</script>

<template>
  <section class="sub-header h-19 flex justify-between items-center">
    <span class="font-600">"Самое новое"</span>

    <div class="link flex items-center">
      <a
        class="font-500 mr-2"
        href="#"
      >
        Смотреть все
      </a>

      <span class="icon mt-1"><IconRight /></span>
    </div>
  </section>
</template>

<style lang="scss" scoped>
.sub-header {
  font-size: 1.3rem;

  .link,
  .link > span {
    color: var(--vt-c-indigo-light);
    cursor: pointer;

    &:hover {
      color: var(--vt-c-yellow);
    }

    &:active {
      color: var(--color-btn);
    }

    &:disabled {
      color: var(--vt-c-gray-mute);
    }
  }

  .icon {
    color: var(--vt-c-indigo-light);
  }
}
</style>
