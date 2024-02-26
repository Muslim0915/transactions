<script setup>

import TransactionBalance from "@/components/TransactionBalance.vue";
import TransactionHistory from "@/components/TransactionHistory.vue";
import TransactionForm from "@/components/TransactionForm.vue";
import {computed, onMounted, ref} from "vue";
import IncomeExpenses from "@/components/IncomeExpenses.vue";
import {useToast} from "vue-toastification";

const transactions = ref([
  {id: 1, title: 'Groceries', amount: -20},
  {id: 2, title: 'Cinema', amount: 20},
  {id: 3, title: 'Books', amount: -10},
]);
const toast = useToast();

let saveTransactionData = () => localStorage.setItem('transactions', JSON.stringify(transactions.value));

onMounted(()=>{
  const savedTransactions = JSON.parse(localStorage.getItem('transactions'))
  if (savedTransactions){
    transactions.value = savedTransactions;
  }
})


const totalIncome = computed(() => {
  return transactions.value
      .filter((transaction) => transaction.amount > 0)
      .reduce((acc, transaction) => acc + transaction.amount, 0)
      .toFixed(2);
});

const totalExpense = computed(() => {
  return transactions.value
      .filter((transaction) => transaction.amount < 0)
      .reduce((acc, transaction) => acc + transaction.amount, 0)
      .toFixed(2);
});

const totalBalance = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0).toFixed(2);
});
const addTransaction = (data) => {
  transactions.value.push({
    id: Date.now(),
    title: data.title,
    amount: data.amount,
  });
  toast.success('Transaction added');
  saveTransactionData();
}

const deleteTransaction = (id) => {
  transactions.value = transactions.value.filter((transaction) => transaction.id !== id);
  toast.success('Transaction deleted')
  saveTransactionData();
}

</script>
<template>
  <div class="app">
    <h1 class="title">Expense Tracker</h1>
    <TransactionBalance :total="totalBalance"/>
    <IncomeExpenses :expense="+totalExpense" :income="+totalIncome"/>
    <div class="transaction-history">
      <h2 class="section-title">
        History
      </h2>
      <TransactionHistory
          v-for="transaction in transactions"
          :key="transaction.id"
          :amount="transaction.amount"
          :class="transaction.amount < 0 ? 'minus' : 'plus'"
          :title="transaction.title"
          @deleteTransaction="deleteTransaction(transaction.id)"
      />
    </div>
    <TransactionForm @addTransaction="addTransaction"/>
  </div>
</template>


<style lang="scss" scoped>

.transaction-history {
  display: flex;
  flex-direction: column;
  gap: 20px;
}
</style>