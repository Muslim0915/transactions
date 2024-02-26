<script setup>

const props = defineProps({
  income: {
    type: Number,
    required: true,
  },
  expense: {
    type: Number,
    required: true,
  }
})
</script>

<template>
  <div class="income-expense__container">
    <div class="income-expense__item">
      <h4 class="income__title">
        Income
      </h4>
      <p class="income__amount">
        +$ {{props.income}}
      </p>
    </div>
    <div class="income-expense__item">
      <h4 class="expense__title">
        Expense
      </h4>
      <p class="expense__amount">
        -$ {{props.expense}}
      </p>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.income-expense__container{
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 30px;
  background-color: #ffffff;
  border: 1px solid #ccc;
  padding: 10px;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
}
.income-expense__item{
  display: flex;
  flex-direction: column;
  align-items: center;
  text-transform: uppercase;
  font-size: 20px;
  line-height: 30px;
  &:first-child{
    position: relative;
    &::after{
      content: '';
      position: absolute;
      right: -18%;
      top: 0;
      width: 1px;
      height: 100%;
      background-color: #ccc;
    }
  }
}
.income__amount{
  color: #2ecc71;
}
.expense__amount {
  color: #e74c3c;
}

</style>