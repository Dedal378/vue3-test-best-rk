<script setup>
import { ref } from 'vue'
import IconVertical from './icons/IconVertical.vue'
import IconFavOutline from './icons/IconFavOutline.vue'

defineProps({
  fav: {
    type: Boolean,
    required: false,
    default: false,
  },
})
defineEmits(['toggleFav'])

const isDelivery = ref(true)
const isDiscount = ref(true)
</script>

<template>
  <div class="card min-w-100 mr-4 shadow-xl rounded-2xl">
    <div class="card-header relative">
      <div
        v-if="isDiscount"
        class="badge-discount rounded-md shadow-md flex items-center px-2 py-1 absolute left-0 z-1"
      >
        <span><IconVertical /></span>
        <p>Скидка до 7%</p>
      </div>

      <div class="overflow-hidden">
        <div
          v-if="isDelivery"
          class="badge-delivery absolute right-0 z-2"
        >
          <span>Есть<br />доставка</span>
        </div>

        <img
          class="rounded-2xl max-h-62"
          alt="image"
          src="https://picsum.photos/300/200?random=1.webp"
        />
      </div>
    </div>

    <div class="card-body p-2">
      <h4 class="card-title font-bold text-lg leading-6">
        Используйте промокод со скидкой 7% на АКБ
      </h4>
      <img
        alt="logo"
        class="w-24"
        src="../../assets/icons/logo.svg"
      />

      <div class="card-footer flex flex-col">
        <h4 class="text-2xl">Мегафон</h4>

        <div class="flex justify-between">
          <p class="address max-w-75">
            <span>Ближайшее:</span>
            Ярославль, улица Полушкина Роща, 16с71 (1 162 км)
          </p>

          <span class="w-14 cursor-pointer flex justify-center">
            <IconFavOutline
              :class="{ active: fav }"
              @click="$emit('toggleFav')"
            />
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.card {
  background-color: var(--vt-c-white);

  &-header {
    .badge-discount {
      color: var(--vt-c-white);
      font-size: 1rem;
      background-color: var(--vt-c-yellow);
      transform: translateY(-8px) translateX(15px);
    }

    .badge-delivery {
      padding: 8px 25px;
      color: var(--vt-c-white);
      font-size: 0.9rem;
      line-height: 75%;
      background-color: var(--color-background-badge);
      text-align: center;
      transform: rotate(45deg) translateY(-20px) translateX(30px);

      & span {
        font-weight: 700;
      }
    }

    img {
      border: 2px solid var(--vt-c-gray-soft);
      width: 100%;
    }
  }

  &-footer {
    .address,
    span {
      color: var(--vt-c-gray);
      font-weight: 600;
    }

    & .active {
      fill: var(--color-fav);
    }
  }
}
</style>
