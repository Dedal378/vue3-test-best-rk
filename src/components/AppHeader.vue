<script setup>
import { computed, reactive, ref, onMounted } from 'vue'
import { useSelect } from '../use/useSelect.js'
import BaseButton from './ui/BaseButton.vue'
import IconApp from './ui/icons/IconApps.vue'
// import IconGrid from './ui/icons/IconGrid.vue'
// import IconRestaurant from './ui/icons/IconRestaurant.vue'
// import IconBottle from './ui/icons/IconBottle.vue'
// import IconFavOutline from './ui/icons/IconFavOutline.vue'
// import IconStar from './ui/icons/IconStar.vue'

const { activeEl, toggle } = useSelect()

let scrollTop = document.documentElement.scrollTop
const isShown = ref(false)
const input = ref('')

const items = reactive([
  { id: 0, icon: 'IconApp', title: 'Подборки' },
  { id: 1, icon: 'IconGrid', title: 'Все категории' },
  { id: 2, icon: 'IconRestaurant', title: 'Где поесть' },
  { id: 3, icon: 'IconBottle', title: 'Магазины' },
  { id: 4, icon: 'IconFavOutline', title: 'Подборки' },
  { id: 5, icon: 'IconStar', title: 'Где поесть' },
])

const onScroll = () => {
  isShown.value = document.documentElement.scrollTop < scrollTop
  scrollTop = document.documentElement.scrollTop
}
const inputFilter = computed(() =>
  items.filter((el) => input.value === '' || el.title.toLowerCase().indexOf(input.value.toLowerCase()) !== -1)
)

onMounted(() => {
  window.addEventListener('scroll', onScroll)
})
</script>

<template>
  <nav
    :class="{ 'h-80px': isShown }"
    class="navigation sticky overflow-y-hidden flex flex-col z-99 transform-gpu transition-all duration-200 ease-in"
  >
    <div class="wrapper-input">
      <input
        v-model.lazy="input"
        class="input px-5 py-3 rounded-xl min-w-full"
        id="search"
        name="search"
        placeholder="Поиск по всем категориям"
        type="search"
      />
      <span class="icon">
        <svg
          fill="currentColor"
          height="18"
          viewBox="0 0 16 16"
          width="18"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M11.742 10.344a6.5 6.5 0 1 0-1.397 1.398h-.001c.03.04.062.078.098.115l3.85 3.85a1 1 0 0 0 1.415-1.414l-3.85-3.85a1.007 1.007 0 0 0-.115-.1zM12 6.5a5.5 5.5 0 1 1-11 0 5.5 5.5 0 0 1 11 0z"
          />
        </svg>
      </span>
    </div>

    <div class="flex item-center">
      <div
        :class="{ '-translate-y-150px': isShown }"
        class="flex items-center overflow-y-scroll overflow-y-hidden"
      >
        <BaseButton
          v-for="item in inputFilter"
          :key="item.id"
          @click="toggle(item.id)"
          :class="{ 'btn-active': activeEl.includes(item.id) }"
          :icon-left="IconApp"
          :title="item.title"
          class="mr-2"
        />
        <!--        <BaseButton
                  :icon-left="IconApp"
                  title="Подборки"
                  class="mr-2"
                  :class="{ 'btn-active': classActive }"
                  @click="toggle"
                />
                <BaseButton
                  :icon-left="IconGrid"
                  class="mr-2"
                  title="Все категории"
                  :class="{ 'btn-active': classActive }"
                  @click="toggle"
                />
                <BaseButton
                  :icon-left="IconRestaurant"
                  class="mr-2"
                  title="Где поесть"
                  :class="{ 'btn-active': classActive }"
                  @click="toggle"
                />
                <BaseButton
                  :icon-left="IconBottle"
                  class="mr-2"
                  title="Магазины"
                  :class="{ 'btn-active': classActive }"
                  @click="toggle"
                />
                <BaseButton
                  :icon-left="IconFavOutline"
                  class="mr-2"
                  title="Подборки"
                  :class="{ 'btn-active': classActive }"
                  @click="toggle"
                />
                <BaseButton
                  :icon-left="IconStar"
                  class="mr-2"
                  title="Все категории"
                  :class="{ 'btn-active': classActive }"
                  @click="toggle"
                />
                <BaseButton
                  :icon-left="IconVertical"
                  class="mr-2"
                  title="Где поесть"
                  :class="{ 'btn-active': classActive }"
                  @click="toggle"
                />-->
      </div>
    </div>
  </nav>
</template>

<style lang="scss" scoped>
.navigation {
  padding-bottom: 1.3rem;
  padding-left: 1rem;

  .wrapper-input {
    position: relative;
    margin-top: 0.5rem;
    margin-bottom: 1rem;
    padding: 0 1rem 1rem 0;

    & input {
      background-color: var(--vt-c-gray-soft);
      border: 1px solid var(--vt-c-gray-soft);
      outline: 0;

      &::placeholder {
        color: var(--vt-c-gray-mute);
        font-size: 1.3rem;
      }

      &:focus {
        outline: 2px solid var(--vt-c-gray-soft);
        box-shadow: inset 0 0 4px 1px var(--vt-c-gray-mute);
      }

      &:active {
        border: 1px solid var(--vt-c-gray);
      }
    }

    & .icon {
      position: absolute;
      top: 0;
      right: 1.9rem;
      bottom: 1rem;
      display: flex;
      align-items: center;
      width: 1.2rem;
      color: var(--vt-c-gray);
      cursor: pointer;
      transition: color 0.15s ease-in-out;

      &:hover {
        color: var(--vt-c-black-soft);
      }
    }
  }

  .btn-active {
    color: var(--vt-c-white-soft);
    background-color: var(--color-background-active);
    border: 2px solid var(--color-background-active);
    fill: white;
  }
}
</style>
