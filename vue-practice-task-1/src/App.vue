<script>
import ProductCard from "@/components/ProductCard.vue";

export default {
  components: {
    ProductCard,
  },
  data () {
    return {
      cart: [],
    }
  },
  methods: {
    updateCart(id) {
      this.cart.push(id);
    },
    removeFromCart(id) {
      const index = this.cart.indexOf(id);
      if (index > -1) {
        this.cart.splice(index, 1);
      }
    }
  }
};
</script>

<template>
  <div>
    <div class="cart">
    </div>
    <ProductCard
        :cart="cart"
        @remove-from-cart="removeFromCart"
        @add-to-cart="updateCart"></ProductCard>
  </div>
</template>
