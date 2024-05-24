<template>
  <h3>Transaction History</h3>
  <ul class="list">
    <li 
    v-for="transaction in transactions" 
    :key="transaction.id"
    :class="transaction.amount < 0 ? 'minus' : 'plus'"
    >
      {{ transaction.item }} <span>${{transaction.amount}}</span>
      <button class="delete-btn" @click="onClick(transaction.id)">x</button>
    </li>
  </ul>
</template>

<script setup>

 defineProps({
    transactions:{
      type: Array,
      required: true
    }
  })

  const emit = defineEmits(['transactionDeleted'])

  const onClick = (id) => {
    emit('transactionDeleted', id)
  }

</script>