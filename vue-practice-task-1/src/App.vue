<template>
  <div class="product">
    <div class="product-image">
      <img :alt="altText" :src="image" />
    </div>
      <div class="product-info">
        <h1>{{ title }}</h1>
        <p>{{ description }}</p>
        <ul>
          <li v-for="detail in details">{{ detail }}</li>
        </ul>
        <div
            class="color-box"
            v-for="(variant, index) in variants"
            :key="variant.variantId"
            :style="{ backgroundColor:variant.variantColor }"
            @mouseover="updateProduct(index)"
        >
        </div>
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
        <div class="cart">
          <p>Cart({{ cart }})</p>
        </div>
        <br><button
          v-on:click="addToCart"
          :disabled="!inStock"
          :class="{ disabledButton: !inStock }"
      >Add to cart</button>
        <br><button @click="deleteFromCart">Delete one from cart</button>
      </div>
  </div>
</template>

<!--разместил тут и далее этот код пользуясь станлартом vue3(Options api)-->
<script>
export default {
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
      details: ['80% cotton', '20% polyester', 'Gender-neutral'],
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
      cart: 0,
    };
  },
  methods: {
    addToCart () {
      this.cart += 1;
    },
    updateProduct (index) {
      this.selectedVariant = index;
      console.log(index);
    },
    deleteFromCart () {
      this.cart -= 1;
    }
  },
  computed: {
    title() {
      return this.brand + ' ' + this.product;
    },
    image() {
      return this.variants[this.selectedVariant].variantImage;
    },
    inStock(){
      return this.variants[this.selectedVariant].variantQuantity
    },
    onSale() {
      if (this.sale===true && this.variants[this.selectedVariant].variantQuantity <= 100 && this.variants[this.selectedVariant].variantQuantity >=1  ) {
        return this.brand + ' ' + this.product + ' IS ON BIG SALEE!!!'
      }
      else {
      }
    }
  }
};
</script>
