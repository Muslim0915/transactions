<script setup>

import {ref} from "vue";
import {useToast} from "vue-toastification";
import AppButton from "@/components/UI/AppButton.vue";


const toast = useToast();

let title = ref('')
let amount = ref('')
const emit = defineEmits([
  'addTransaction',
]);


const addTransaction = () => {
  if (!title.value || !amount.value) return toast.error('Both fields must be completed')

  const transaction = {
    title: title.value,
    amount: parseFloat(amount.value),
  }
  emit('addTransaction', transaction)
  title.value = ''
  amount.value = ''
}

const props = defineProps({
  isEditable: {
    type: Boolean,
    default: false
  }
})

</script>

<template>
  <form action="#" class="expense-form" @submit.prevent="addTransaction">
    <h2 class="section-title">
      Add new transaction
    </h2>
    <div class="form-control">
      <label for="title">Text</label>
      <input id="title" v-model="title" placeholder="Enter transaction text" type="text"/>
    </div>
    <div class="form-control">
      <label for="amount">Amount</label>
      <input id="amount" v-model="amount" placeholder="Enter transaction amount" step="0.00000000000001" type="number"/>
    </div>
    <div class="form-control">
      <AppButton :value="'Add transaction'" class="submit-button" type="submit"/>
    </div>
  </form>
</template>

<style lang="scss" scoped>
.submit-button {
  background-color: #9C88FF;
  &:hover{
    background-color: #7a66ff;
  }
}

</style>