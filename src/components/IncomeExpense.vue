<template>
    <div class="inc-exp-container">
      <div>
        <h4>Income</h4>
        <p id="money-plus">+${{income}} </p>
      </div>
      <div>
        <h4>Income</h4>
        <p id="money-minus">-${{Math.abs(expense)}}</p>
      </div>

    </div>
</template>

<script setup>

defineProps({
  income: {
    type: Number,
    required: true
  },
  expense: {
    type: Number,
    required: false
  }
})

</script>