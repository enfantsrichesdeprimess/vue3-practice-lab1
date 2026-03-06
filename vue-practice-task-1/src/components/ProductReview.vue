<script>
export default {
  data() {
    return {
      name: null,
      review: null,
      rating: null,
    }
  },
  methods: {
    onSubmit() {
      let ProductReview = {
        name: this.name,
        review: this.review,
        rating: this.rating,
      }
      this.$emit('submit', ProductReview)
      this.name = null
      this.review = null
      this.rating = null
    }
  }
}
</script>

<template>
  <form class="review-form" @submit.prevent="onSubmit">
    <p>
      <label for="name">Name:</label>
      <input id="name" v-model="name" placeholder="name">
    </p>

    <p>
      <label for="review">Review:</label>
      <textarea id="review" v-model="review"></textarea>
    </p>
    <p>
      <label for="rating">Rating:</label>
      <select id="rating" v-model.number="rating">
        <option>5</option>
        <option>4</option>
        <option>3</option>
        <option>2</option>
        <option>1</option>
      </select>
    </p>

    <p>
      <input type="submit" value="Submit">
    </p>
  </form>

</template>
