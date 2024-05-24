<template>
  <Notifications />
  <Header/>
  <div class="container">
    <Balance :total/>
    <IncomeExpense :expense="+expense" :income="+income"/>
    <TransactionList 
    :transactions="transactions" 
    @transactionDeleted="handleTransactionDeleted"
    />
    <AddTransaction @transactionSubmitted="handleTransactionSubmitted"/>
  </div>
</template>

<script setup>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import IncomeExpense from './components/IncomeExpense.vue';
import TransactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';

import { useNotification } from "@kyvg/vue3-notification";

const notification = useNotification()

import { computed, ref } from 'vue'
const transactions = ref([])

// Get Total
const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0);
})

// Get income
const income = computed(() => {
  return transactions.value
  .filter( t => t.amount > 0)
  .reduce((acc, transaction) => acc + transaction.amount, 0)
  .toFixed(2)
})

// Get expense
const expense = computed(() => {
  return transactions.value
  .filter( t => t.amount < 0)
  .reduce((acc, transaction) => acc + transaction.amount, 0)
  .toFixed(2)
})

// Add transaction
const handleTransactionSubmitted = (transactionData) => {
    console.log('receive data from emit', transactionData)
    transactions.value.push({
      id: crypto.randomUUID(),
      item: transactionData.item,
      amount: transactionData.amount
    })

    notification.notify({
    title:'Transaction added.',
    type: 'success'
  })
}

// Delete transaction
const handleTransactionDeleted = (id) => {
  transactions.value = transactions.value.filter(t => t.id !== id)
  notification.notify({
    title:'Transaction deleted.',
    type: 'success'
  })
}
</script>