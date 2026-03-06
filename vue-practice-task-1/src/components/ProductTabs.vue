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
      search: null,
    }
  },
  props: {
    reviews: {
      type: Array,
      required: false
    },
  },
  computed: {
    filtered() {
        if (this.search === null || this.search === '') {
          return this.reviews
        } else {
          return this.reviews.filter(review => {
            return review.name.toLowerCase().includes(this.search.toLowerCase()) ||
            review.review.toLowerCase().includes(this.search.toLowerCase())
          })
        }
    }
  }
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
        <input v-model="search" id="search" placeholder="Search"/>
      <p v-if="!reviews.length">There are no reviews yet.</p>
      <p v-else-if="!filtered.length">No reviews match your search</p>
      <ul>
        <li v-for="review in filtered">
          <p>{{ review.name }}</p>
          <p>Rating: {{ review.rating }}</p>
          <p>{{ review.review }}</p>
          <p>Recomended:{{ review.recommend }}</p>
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