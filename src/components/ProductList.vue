<template>
    <div class="product-grid">
      <div class="product-card" v-for="product in productStore.products" :key="product.id">
        <img :src="product.image" alt="product image" class="product-image" />
        <h2 class="product-title">{{ product.name }}</h2>
        <p class="product-description">
          {{ product.description }}
        </p>
        <div class="product-footer">
          <span class="instock">InStock : {{ product.instock }}</span>
          <button @click="addToCart(product)" class="add-to-cart">
            AddToCart
          </button>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { onMounted } from 'vue'
  import { useProductStore } from '../store/productStore'
  import { useCartStore } from '../store/cartStore'
  
  const productStore = useProductStore()
  const cartStore = useCartStore()
  
  onMounted(() => {
    productStore.fetchProducts()
  })
  
  const addToCart = (product) => {
  if (product.instock > 0) {
    cartStore.addToCart(product)
    product.instock-- 
  } else {
    alert('This product is out of stock!')
  }
}
  </script>
  
  <style scoped>
  .product-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
    gap: 1rem;
    padding: 1rem;
  }
  
  .product-card {
    border: 1px solid #ccc;
    border-radius: 10px;
    padding: 1rem;
    text-align: center;
    background: white;
    box-shadow: 0 2px 6px rgba(0,0,0,0.1);
  }
  
  .product-image {
    width: 100%;
    height: 200px;
    object-fit: cover;
    border-radius: 6px;
    margin-bottom: 10px;
  }
  
  .product-title {
    font-size: 1.25rem;
    margin: 0.5rem 0;
  }
  
  .product-description {
    font-size: 0.95rem;
    text-align: justify;
    color: #444;
  }
  
  .product-footer {
    margin-top: 1rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  
  .instock {
    color: green;
    font-weight: bold;
  }
  
  .add-to-cart {
    background-color: #007bff;
    color: white;
    border: none;
    padding: 0.4rem 1rem;
    border-radius: 5px;
    cursor: pointer;
  }
  
  .add-to-cart:hover {
    background-color: #0056b3;
  }
  </style>
  