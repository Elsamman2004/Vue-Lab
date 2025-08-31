<template>
  <div>
    <!-- Navbar -->
    <Navbar 
  :cart="cart" 
  :total-price="totalPrice" 
  :discount="discount"
  @remove-from-cart="removeFromCart" 
/>


    <div class="container my-4">
      <!-- رسالة الخصم -->
      <div v-if="discount > 0" class="alert alert-success text-center">
        🎉 Special Offer: {{ discount }}% OFF on selected items!
      </div>

      <!-- زرار إظهار/إخفاء المنتجات -->
      <div class="text-center mb-3">
        <button class="btn btn-outline-primary" @click="showProducts = !showProducts">
          {{ showProducts ? 'Hide Products' : 'Show Products' }}
        </button>
      </div>

      <!-- المنتجات -->
      <div v-show="showProducts" class="row">
        <ProductCard
          v-for="product in products"
          :key="product.id"
          :product="product"
          @add-to-cart="addToCart"
        />
      </div>

      <!-- لو مفيش منتجات -->
      <div v-if="products.length === 0" class="text-center mt-5">
        <p class="text-muted">🚫 No products available</p>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "./components/Navbar.vue";
import ProductCard from "./components/ProductCard.vue";

export default {
  name: "App",
  components: { Navbar, ProductCard },
  data() {
    return {
      products: [],
      cart: [],
      cartCount: 0,
      showProducts: true,
      discount: 10,
    };
  },
  async mounted() {
    // ✅ DummyJSON API بدل FakeStore
    const res = await fetch("https://dummyjson.com/products?limit=12");
    const data = await res.json();
    this.products = data.products;
  },
  methods: {
    addToCart(product) {
      this.cart.push(product);
      this.cartCount++;
alert(`${product.title} added to cart!`);
    },
    removeFromCart(index) {
      this.cart.splice(index, 1);
      this.cartCount--;
    },
  },
  computed: {
    totalPrice() {
      return this.cart.reduce((total, item) => total + item.price, 0);
    },
  },
};
</script>