<template>
  <h1>{{ product }}</h1>
  <p>{{ description }}</p>
</template>

<!--разместил тут и далее этот код пользуясь станлартом vue3(Options api)-->
<script>
export default {
  data() {
    return {
      product: 'Socks',
      description: 'A pair of warm, fuzzy socks'
    };
  },
};
</script>
