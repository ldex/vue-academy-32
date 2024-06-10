<script setup>
import { ref } from 'vue'
import ProductList from '@/components/ProductList.vue'
import ProductService from '@/services/ProductService.js'

let products = ref([])
const errorMessage = ref(null)
const isLoading = ref(false)

isLoading.value = true
ProductService.getProducts()
  .then(data => products.value = data)
  .catch(error => {
    errorMessage.value = 'There was an error getting products from server, ' + error
  })
  .finally(() => isLoading.value = false)
</script>

<template>
  <div id="app">
    <h1>Vue Store</h1>
    <nav>
      <router-link to="/">Home</router-link>
      <router-link to="/products">Products</router-link>
      <router-link to="/about">About</router-link>
    </nav>
    <router-view />
    <hr />
    <footer>Copyright Vue Academy 2024</footer>
  </div>
</template>

<style scoped></style>
