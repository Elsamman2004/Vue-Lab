<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark shadow-sm py-3">
    <div class="container-fluid">
      <a class="navbar-brand d-flex align-items-center" href="#">
        <img src="/favicon.ico" alt="Logo" width="32" class="me-2" />
        Vue Store
      </a>
      <div class="d-flex">
        <Cart 
          :cart="cart" 
          :total-price="totalPrice" 
          :discount="discount"
          @remove-from-cart="$emit('remove-from-cart', $event)" 
        />
      </div>
    </div>
  </nav>
</template>

<script>
import Cart from "./Cart.vue";

export default {
  name: "Navbar",
  components: { Cart },
  props: {
    cart: Array,
    totalPrice: Number,   
    discount: Number      
  }
};
</script>

<!-- أضف هذا داخل <head> في index.html -->
<link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700&display=swap" rel="stylesheet">
<style>
  body {
    font-family: 'Cairo', Arial, sans-serif;
    background: #f8f9fa;
  }
  .card-img-top {
    border-radius: 0.75rem 0.75rem 0 0;
    height: 220px;
    object-fit: cover;
  }
  .card:hover {
    transform: translateY(-5px) scale(1.02);
    box-shadow: 0 8px 24px rgba(0,0,0,0.12);
    transition: 0.2s;
  }
  .modal-content {
    border-radius: 1rem;
    box-shadow: 0 8px 32px rgba(0,0,0,0.15);
  }
  .btn-success {
    font-size: 1.1rem;
    padding: 0.5rem 2rem;
    border-radius: 2rem;
  }
</style>
