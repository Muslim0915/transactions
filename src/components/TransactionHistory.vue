<script setup>

import AppButton from "@/components/UI/AppButton.vue";

const props = defineProps({
  title:{
    type: String,
    required: true,
  },
  amount:{
    type: Number,
    required: true,
  },
});

const emit = defineEmits(['deleteTransaction']);


</script>

<template>
  <div class="transaction-history__item">
    <h3 class="transaction-history__title">
      {{props.title}}
      $ {{props.amount}}
    </h3>
      <AppButton value="Delete" class="delete-button" @click="emit('deleteTransaction')"/>
  </div>
</template>

<style scoped lang="scss">
.transaction-history__item{
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  gap: 30px;
  border-radius: 5px;
  background-color: #ffffff;
  border: 1px solid #ccc;
  position: relative;
  text-transform: capitalize;
}
.plus::after,
.minus::after{
  content: '';
  position: absolute;
  right: 0;
  top: 0;
  width: 5px;
  height: 100%;
}
.plus::after{
  background-color: #2ecc71;
}
.minus::after{
  background-color: #e74c3c;
}
.transaction-history__buttons{
  display: flex;
  align-items: center;
  gap: 10px;
}
.delete-button{
  background-color: #e74c3c;
  &:hover{
    background-color: #c0392b;
  }
}
</style>