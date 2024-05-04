<template>
  <h3>History</h3>
  <ul id="list" class="list">
    <li
      v-for="tran in transactions"
      v-bind:key="tran.id"
      :class="tran.amount < 0 ? 'minus' : 'plus'"
    >
      {{ tran.text }} <span>{{ tran.amount }}</span
      ><button class="delete-btn">x</button>
    </li>
  </ul>
</template>

<script setup>
const props = defineProps({
  transactions: {
    type: Array,
    required: true,
  },
});
</script>
