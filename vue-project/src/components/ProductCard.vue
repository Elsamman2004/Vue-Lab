<template>
  <div class="col-md-4 mb-4">
    <div class="card h-100 shadow-sm">
      <img :src="product.thumbnail" class="card-img-top" :alt="product.title" />

      <div class="card-body">
        <h5
          class="card-title"
          :class="{
            'text-muted': product.stock === 0,
            'text-success': product.stock > 50,
            'text-warning': product.stock > 0 && product.stock <= 50
          }"
        >
          {{ product.title }}
        </h5>

        <p class="card-text">{{ product.description }}</p>
        <p class="fw-bold">${{ product.price }}</p>

        <p>
          <span v-if="product.stock > 50" class="text-success">In Stock</span>
          <span v-else-if="product.stock > 0" class="text-warning">Limited Stock</span>
          <span v-else class="text-danger">Out of Stock</span>
        </p>

        <button
          class="btn btn-primary"
          :disabled="product.stock === 0"
          @click="$emit('add-to-cart', product)"
        >
          Add to Cart
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProductCard",
  props: {
    product: Object,
  },
};
</script>
