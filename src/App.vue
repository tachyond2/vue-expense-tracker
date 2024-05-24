<template>
  <Notifications />
  <Header/>
  <div class="container">
    <Balance/>
    <IncomeExpense/>
    <TransactionList :transactions="transactions"/>
    <AddTransaction @transactionSubmitted="handleTransactionSubmitted"/>
  </div>
</template>

<script setup>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import IncomeExpense from './components/IncomeExpense.vue';
import TransactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';


import { ref } from 'vue'
const transactions = ref([])


const handleTransactionSubmitted = (transactionData) => {
    console.log('receive data from emit', transactionData)
    transactions.value.push({
      id: crypto.randomUUID(),
      item: transactionData.item,
      amount: transactionData.amount
    })
}
</script>