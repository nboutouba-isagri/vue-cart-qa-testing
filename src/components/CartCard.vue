<script setup lang="ts">
import { useCartStore } from '@/store/cart'
import type { CartPreview } from '@/store/cart'
import { toCurrency } from '@/shared/utils'

defineProps<{
  cartProduct: CartPreview
}>()

const cartStore = useCartStore()
</script>

<template>
  <div class="card md:card-side bordered">
    <figure class="p-8">
      <img
        :src="cartProduct.image"
        alt="Card Image"
        class="object-contain w-full h-48"
      >
    </figure>
    <div class="card-body">
      <h2 class="card-title">
        <router-link class="link link-hover" :to="`/product/${cartProduct.id}`">
          {{ cartProduct.title }}
        </router-link>
      </h2>
      <p>{{ toCurrency(cartProduct.cost) }}</p>
      <div class="card-actions">
        <div class="btn-group">
          <button class="btn btn-primary" @click="cartStore.remove(cartProduct.id)" :data-cy="`module_cartcard_button_remove-product-${cartProduct.id}`">
            -
          </button>
          <button class="btn btn-ghost no-animation">
            {{ cartProduct.quantity }}
          </button>
          <button class="btn btn-primary" @click="cartStore.add(cartProduct.id)" :data-cy="`module_cartcard_button_add-product-${cartProduct.id}`">
            +
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
