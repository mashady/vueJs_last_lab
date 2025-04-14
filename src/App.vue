<template>
  <div class="">
    <nav>
      <router-link to="/">Home</router-link> |
      <router-link to="/products">Products</router-link> |
      <router-link to="/cart">Cart</router-link>
    </nav>
    <router-view />
  </div>
</template>

<script setup></script>

<style scoped>
nav {
  padding: 1rem;
}
nav a {
  margin: 0 1rem;
  text-decoration: none;
  color: #333;
}
</style>
