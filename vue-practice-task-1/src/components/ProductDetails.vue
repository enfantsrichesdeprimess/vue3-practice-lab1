<script>
export default {
  data() {
    return {

    }
  },
  props: {
    detail: {
      type: String,
      required: true
    }
  }
}
</script>

<template>
  <li>{{ detail }}</li>
</template>
