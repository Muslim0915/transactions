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

.balance{
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  gap: 10px;
  position: relative;
  text-transform: capitalize;
  .balance-currency{
    font-size: 30px;
    line-height: 40px;
  }
}

</style>