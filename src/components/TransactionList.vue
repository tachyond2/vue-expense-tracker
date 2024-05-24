<template>
  <h3>Transaction History</h3>
  <ul class="list">
    <li 
    v-for="transaction in transactions" 
    :key="transaction.id"
    :class="transaction.amount < 0 ? 'minus' : 'plus'"
    >
      {{ transaction.item }} <span>${{transaction.amount}}</span>
      <button class="delete-btn">x</button>
    </li>
  </ul>
</template>

<script setup>

  const props = defineProps({
    transactions:{
      type: Array,
      required: true
    }
  })
</script>