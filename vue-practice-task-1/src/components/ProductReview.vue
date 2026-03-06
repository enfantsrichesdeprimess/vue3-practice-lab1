<script>
export default {
  data() {
    return {
      name: null,
      review: null,
      rating: null,
      recommended: null,
      errors: [],
    }
  },
  methods: {
    onSubmit() {
      if(this.name && this.review && this.rating) {
        let productReview = {
          name: this.name,
          review: this.review,
          rating: this.rating,
          recommended: this.recommended
        }
        this.$emit('submit-review', productReview)
        this.name = null
        this.review = null
        this.rating = null
        this.recommended = null
      } else {
        if(!this.name) this.errors.push("Name required.")
        if(!this.review) this.errors.push("Review required.")
        if(!this.rating) this.errors.push("Rating required.")
        if(!this.recommended) this.errors.push("Recommended required.")
      }

    }
  }
}
</script>

<template>
  <form class="review-form" @submit.prevent="onSubmit">
    <p v-if="errors.length">
      <b>Please correct the following error(s):</b>
      <ul>
        <li v-for="error in errors">{{ error }}</li>
      </ul>
    </p>
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
      <label>Would you recommend this product?</label><br>
      <input
          type="radio"
          id="recommend-yes"
          value="yes"
          v-model="recommended"
      >
      <label for="recommend-yes">Yes</label>

      <input
          type="radio"
          id="recommend-no"
          value="no"
          v-model="recommended"
      >
      <label for="recommend-no">Noooo</label>
    </p>
    <p>
      <input type="submit" value="Submit">
    </p>
  </form>
</template>
