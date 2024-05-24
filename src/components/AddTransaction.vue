<template>
  <h3>Add new transaction</h3>
  <form  id="form" @submit.prevent="onSubmit">
    <div class="form-control">
      <label for="item" >Item</label>
      <input type="text" id="item" placeholder="Enter transaction..." v-model="item"/>
    </div>
    <div class="form-control">
      <label for="amount" >amoun<br/>
        (negative - expense, positive - income)</label>
      <input type="text" id="amount" placeholder="Enter amount..." v-model="amount"/>
    </div>
    <button class="btn">Add transaction</button>
  </form>
</template>

<script setup>
import { ref } from 'vue'
import { useNotification } from "@kyvg/vue3-notification";

const notification = useNotification()



  const item = ref('')
  const amount = ref('')
  const emit = defineEmits(['transactionSubmitted'])

const onSubmit = () => {
  if(!item.value || !amount.value){
    notification.notify({
      title: "Both fields must be filled",
      // type: 'error',
    });
    return
  }
  console.log('received data from form: ',item.value, amount.value )
  const transactionDate = {
    item: item.value,
    amount: parseFloat(amount.value)
  }
  emit('transactionSubmitted', transactionDate)
}
</script>