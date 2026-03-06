<script>
import ProductReview from "@/components/ProductReview.vue";
import ProductDetails from "@/components/ProductDetails.vue";
import eventBus from '../eventBus'
import ProductShipping from "@/components/ProductShipping.vue";

export default {
  components: {
    ProductShipping,
    ProductReview,
    ProductDetails,
  },
  data() {
    return {
      tabs: ['Reviews', 'Make a Review', 'Shipping', 'Details'],
      selectedTab: 'Reviews',
      details: ['80% cotton', '20% polyester', 'Gender-neutral'],
      premium: true,

    }
  },
  props: {
    reviews: {
      type: Array,
      required: false
    },
  },
  methods: {
    addReview(productReview) {
      this.reviews.push(productReview)
    },
  },
}
</script>

<template>
  <div>
    <ul>
         <span class="tab"
               :class="{ activeTab: selectedTab === tab }"
               v-for="(tab, index) in tabs"
               @click="selectedTab = tab"
         >{{ tab }}</span>
    </ul>
    <div v-show="selectedTab === 'Reviews'">
      <p v-if="!reviews.length">There are no reviews yet.</p>
      <ul>
        <li v-for="review in reviews">
          <p>{{ review.name }}</p>
          <p>Rating: {{ review.rating }}</p>
          <p>{{ review.review }}</p>
        </li>
      </ul>
    </div>
    <div v-show="selectedTab === 'Make a Review'">
      <product-review></product-review>
    </div>
    <div v-show="selectedTab === 'Details'">
      <product-details :details="details"></product-details>
    </div>
    <div v-show="selectedTab === 'Shipping'">
      <product-shipping :premium="premium"></product-shipping>
    </div>
  </div>

</template>