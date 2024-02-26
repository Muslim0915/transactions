<script setup>
const props = defineProps({
  total: {
    type: Number,
    required: true
  }
})

</script>

<template>
  <div class="balance">
    <h2 class="section-title">
      Your Balance
    </h2>
    <div class="balance-currency">
      $ <span class="balance-amount">{{props.total}}</span>
    </div>
  </div>
</template>

<style scoped lang="scss">

</style>