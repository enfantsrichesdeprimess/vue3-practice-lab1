<script>
export default {
  props: {
    premium: {
      type: Boolean,
      required: true,
    },
  },
  computed: {
    shipping() {
      if (this.premium) {
        return "Free";
      } else {
        return 2.99
      }
    }
  }
}
</script>

<template>
  <p>Shipping: {{ shipping }}</p>
</template>