<template>
  <div class="inc-exp-container">
    <div>
      <h4>{{ income }}</h4>
      <p id="money-plus" class="money plus">+$</p>
    </div>
    <div>
      <h4>{{ expenses }}</h4>
      <p id="money-minus" class="money minus">-$0.00</p>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  income: {
    type: Number,
    required: true,
  },
  expenses: {
    type: Number,
    required: true,
  },
});
</script>
