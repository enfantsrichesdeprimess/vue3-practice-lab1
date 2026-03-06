<script>
export default {
  props: {
    details: {
      type: String,
      required: true
    }
  }
}
</script>

<template>
  <div>
    <ul>
      <li v-for="detail in details">{{ detail }}</li>
    </ul>
  </div>
</template>
