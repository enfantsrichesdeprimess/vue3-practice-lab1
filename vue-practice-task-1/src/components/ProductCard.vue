<script>
import draggable from 'vuedraggable'
import ProductDetails from "@/components/ProductDetails.vue";
import ProductReview from "@/components/ProductReview.vue";
import ProductTabs from "@/components/ProductTabs.vue";
import eventBus from "@/eventBus.js";

export default {
  components: {
    draggable,
    ProductDetails,
    ProductReview,
    ProductTabs,
  },
  data() {
    return {
      brand: 'Vue Mastery',
      product: 'Socks',
      description: 'A pair of warm, fuzzy socks',
      selectedVariant: 0,
      altText: 'Pair Of Socks',
      link: 'https://www.amazon.com/s/ref=nb_sb_noss?url=search-alias%3Daps&field-keywords=socks',
      inventory: 100,
      sale: true,
      reviews: [],
      variants: [
        {
          variantId: 2234,
          variantColor: 'green',
          variantImage: "assets/socks.jpg",
          variantQuantity: 100
        },
        {
          variantId: 2235,
          variantColor: 'blue',
          variantImage: "assets/bluesocks.jpg",
          variantQuantity: 0
        }
      ],
      sizes: ['S', 'M', 'L', 'XL', 'XXL', 'XXXL'],
    };
  },
  props: {
    cart: {
      type: Array,
      required: true
    },
  },
  methods: {
    addToCart() {
      this.$emit('add-to-cart',
          this.variants[this.selectedVariant].variantId);
    },
    updateProduct(index) {
      this.selectedVariant = index;
      console.log(index);
    },
    removeFromCart() {
      const variantId = this.variants[this.selectedVariant].variantId;
      this.$emit('remove-from-cart', variantId);
    },
    cloneVariant(variant) {
      return {
        ...variant,
        variantId: variant.variantId + Date.now()
      }
    },
    onCartChange(event) {
      console.log('Cart changed:', event);
      if (event.added) {
        const newItem = event.added.element;
        console.log('Added to cart:', newItem);
      }
    }
  },
    computed: {
      title() {
        return this.brand + ' ' + this.product;
      },
      image() {
        return this.variants[this.selectedVariant].variantImage;
      },
      inStock() {
        return this.variants[this.selectedVariant].variantQuantity
      },
      onSale() {
        if (this.sale === true && this.variants[this.selectedVariant].variantQuantity <= 100 && this.variants[this.selectedVariant].variantQuantity >= 1) {
          return this.brand + ' ' + this.product + ' IS ON BIG SALEE!!!'
        } else {
        }
      },
    },
    mounted() {
      eventBus.on('submit-review', (productReview) => {
        console.log('New review received via eventBus:', productReview)
        this.reviews.push(productReview)
      })

      console.log('Product component mounted, listening for reviews...')
    },
    unmounted() {
      eventBus.off('submit-review')
    },
  }
</script>


<template>
  <div class="product">
    <div class="product-image">
      <img :alt="altText" :src="image" />
    </div>
    <div class="product-info">
      <h1>{{ title }}</h1>
      <p>{{ description }}</p>
      <draggable
          :list="variants"
          :group="{ name: 'products', pull: 'clone', put: false }"
          :sort="false"
          :clone="cloneVariant"
          item-key="variantId"
      >
        <template #item="{ element, index }">
          <div
              class="color-box"
              :style="{ backgroundColor: element.variantColor }"
              @mouseover="updateProduct(index)"
          >
          </div>
        </template>
      </draggable>
      <ul>
        <li v-for="size in sizes">{{ size }}</li>
      </ul>
      <div class="sale-text">
        <span>{{ onSale }}</span>
      </div>
      <div>
        <p v-if="inStock > 0">In stock</p>
        <p v-else-if="inStock <= 10 && inStock > 0">Almost sold out!</p>
        <p v-else :class="{ outOfStock: !inStock }">Out of stock</p>
      </div>
      <a :href="link"> More product like this </a>
      <draggable
          :list="cart"
          :group="{ name: 'products', pull: false, put: true }"
          :sort="false"
          @change="onCartChange"
          item-key="variantId"
          class="cart-dropzone"
      >
        <template #item="{ element }">
          <div class="cart-item">
            {{ element.variantColor }} sock
          </div>
        </template>
        <template #header>
          <p>Cart({{ cart.length }})</p>
        </template>
      </draggable>
      <br><button
        v-on:click="addToCart"
        :disabled="!inStock"
        :class="{ disabledButton: !inStock }"
    >Add to cart</button>
      <br><button @click="removeFromCart">Delete one from cart</button>
    </div>
    <product-tabs :reviews="reviews"></product-tabs>
  </div>
</template>
