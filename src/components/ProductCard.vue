<script setup lang="ts">
import { useCartStore } from '@/store/cart'
import type { Product } from '@/store/products'
import { toCurrency } from '@/shared/utils'

defineProps<{
  product: Product
}>()

const cartStore = useCartStore()
</script>

<template>
  <div class="card bordered shadow-lg">
    <figure class="px-8 pt-8">
      <img
        :src="product.image"
        alt="Card Image"
        class="object-contain w-full h-48"
      >
    </figure>
    <div class="card-body">
      <h2 class="card-title">
        <router-link class="link link-hover" :to="`/product/${product.id}`">
          {{ product.title }}
        </router-link>
      </h2>
      <p>{{ toCurrency(product.price) }}</p>
      <div class="justify-end card-actions">
        <button class="btn btn-primary" @click="cartStore.add(product.id)">
          Add to Cart
        </button>
      </div>
    </div>
  </div>
</template>
