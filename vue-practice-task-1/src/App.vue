<template>
  <div class="product">
    <div class="product-image">
      <img :alt="altText" :src="image" />
    </div>
      <div class="product-info">
        <h1>{{ product }}</h1>
        <p>{{ description }}</p>
        <ul>
          <li v-for="detail in details">{{ detail }}</li>
        </ul>
        <div v-for="variant in variants" :key="variant.variantId">
          <p>{{ variant.variantColor }}</p>
        </div>
        <ul>
          <li v-for="size in sizes">{{ size }}</li>
        </ul>
        <div class="sale-text">
          <span v-if="inventory <= 100 && sale === true">Big Sale!!!</span>
          </div>
        <p v-if="inventory > 10">In stock</p>
        <p v-else-if="inventory <= 10 && inventory > 0">Almost sold out!</p>
        <p v-else>Out of stock</p>
        <a :href="link"> More product like this </a>
      </div>
  </div>
</template>

<!--разместил тут и далее этот код пользуясь станлартом vue3(Options api)-->
<script>
export default {
  data() {
    return {
      product: 'Socks',
      description: 'A pair of warm, fuzzy socks',
      image: 'assets/socks.jpg',
      altText: 'Pair Of Greeeeeeeen Socks',
      link: 'https://www.amazon.com/s/ref=nb_sb_noss?url=search-alias%3Daps&field-keywords=socks',
      inStock: true,
      inventory: 100,
      sale: true,
      details: ['80% cotton', '20% polyester', 'Gender-neutral'],
      variants: [
        {
          variantId: 2234,
          variantColor: 'green'
        },
        {
          variantId: 2235,
          variantColor: 'blue'
        }
      ],
      sizes: ['S', 'M', 'L', 'XL', 'XXL', 'XXXL'],
    };
  },
};
</script>
