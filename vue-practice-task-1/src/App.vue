<template>
  <div class="product-image">
    <img :alt="altText" :src="image" />
  </div>
  <div class="product-info">
    <h1>{{ product }}</h1>
    <p>{{ description }}</p>
    <a :href="link"> More product like this </a>
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
    };
  },
};
</script>
