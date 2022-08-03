<script setup>
defineProps({
  //текст кнопки
  title: { type: String, required: true },

  //иконка слева
  iconLeft: { type: Object, default: null, required: false },

  // заблокированная
  disabled: { type: Boolean, default: false, required: false },

  // скругленная
  round: { type: Boolean, default: false, required: false },

  // тип кнопки -> button | reset | submit
  type: { type: String, default: 'button', required: false },

  // стиль кнопки -> default | plain
  mode: { type: String, default: 'default', required: false },

  // прозрачная или залитая
  plain: { type: Boolean, default: false, required: false },
})
</script>

<template>
  <button
    :class="[{ plain, round, 'has-left-icon': iconLeft }, mode]"
    :disabled="disabled"
    :type="type"
    class="base-button"
  >
    <component
      v-if="iconLeft"
      :is="iconLeft"
      class="icon-left"
    />

    <template v-if="title">{{ title }}</template>

    <slot v-else />
  </button>
</template>

<style lang="scss" scoped>
.base-button {
  display: flex;
  flex: 0 0 auto;
  justify-content: center;
  align-items: center;
  min-height: 100%;
  padding: 4px 12px !important;
  color: var(--color-btn);
  font-size: 1.3rem;
  font-weight: 500;
  background-color: var(--vt-c-white);
  border: 2px solid var(--color-border);
  border-radius: 10px;
  outline: 0;
  cursor: pointer;
  transition: background-color 0.15s ease, border 0.15s ease, color 0.15s ease;

  &.has-left-icon {
    padding: 0 24px 0 19px;
  }

  .icon-left {
    width: 32px;
    height: auto;
    padding: 0;
    margin: 0;
    margin-right: 4px;
  }

  &:active {
    color: var(--vt-c-white-soft);
    background-color: var(--color-background-active);
    border: 1px solid var(--color-background-active);
  }

  &:disabled {
    color: var(--vt-c-gray-mute);
    cursor: default;
    opacity: 0.5;

    &:hover {
      color: var(--color-btn);
      background-color: var(--color-background);
      border: 1px solid var(--color-border);
    }

    &:active {
      color: var(--color-btn);
      background-color: var(--color-background);
      border: 1px solid var(--color-border);
    }
  }

  &.round {
    border-radius: 25px;
  }

  &.plain {
    color: var(--vt-c-indigo-light);
    background-color: transparent;

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
}
</style>
