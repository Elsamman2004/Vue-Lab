<template>
  <div>
    <!-- زرار يفتح المودال -->
    <button
      type="button"
      class="btn btn-outline-light position-relative"
      data-bs-toggle="modal"
      data-bs-target="#cartModal"
    >
      🛒 Cart
      <span class="position-absolute top-0 start-100 translate-middle badge rounded-pill bg-danger">
        {{ cart.length }}
      </span>
    </button>

    <!-- المودال -->
    <div
      class="modal fade"
      id="cartModal"
      tabindex="-1"
      aria-labelledby="cartModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog modal-lg">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="cartModalLabel">Your Cart</h5>
            <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
          </div>

          <div class="modal-body">
            <ul class="list-group">
              <li
                v-for="(item, index) in cart"
                :key="index"
                class="list-group-item d-flex justify-content-between align-items-center"
              >
                {{ item.title }} - ${{ item.price }}
                <button class="btn btn-sm btn-danger" @click="$emit('remove-from-cart', index)">
                  Remove
                </button>
              </li>
            </ul>

            <div v-if="cart.length === 0" class="text-center text-muted">
              Your cart is empty 🛒
            </div>
          </div>

          <!-- ✅ Footer مرتب -->
          <div class="modal-footer d-flex justify-content-between w-100">
            <div v-if="cart.length > 0" class="fw-bold">
              Total: ${{ totalPrice.toFixed(2) }}
              <div v-if="discount > 0" class="text-success">
                After Discount: ${{ (totalPrice * (1 - discount / 100)).toFixed(2) }}
              </div>
            </div>
            <button class="btn btn-success" data-bs-dismiss="modal">Checkout</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Cart",
  props: {
    cart: Array,
    totalPrice: Number,
    discount: Number
  }
};
</script>
