<script setup>
import { reactive } from 'vue'
import { useSelect } from '../use/useSelect.js'

import BaseCard from './ui/BaseCard.vue'
import BaseTitle from './ui/BaseTitle.vue'

const { activeEl, toggle } = useSelect()
const items = reactive([{ id: 0 }, { id: 1 }, { id: 2 }, { id: 3 }, { id: 4 }, { id: 5 }])
</script>

<template>
  <BaseTitle class="title" />

  <div class="flex items-center pt-2 pl-4 overflow-y-scroll">
    <BaseCard
      v-for="item in items"
      :key="item.id"
      :fav="activeEl.includes(item.id)"
      @toggle-fav="toggle(item.id)"
    />
  </div>
</template>

<style lang="scss" scoped>
.title {
  padding: 0 1rem;
}
</style>
