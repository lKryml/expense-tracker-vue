<template>
  <Header />
  <div class="container">
    <Balance :total="total" />
    <IncomeExpenses />
    <TransactionList :transactions="transactions" />
    <AddTransaction />
  </div>
</template>

<script setup>
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpenses from "./components/IncomeExpenses.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";

import { ref, computed } from "vue";

const transactions = ref([
  { id: 1, text: "flower", amount: 5 },
  { id: 2, text: "floweer", amount: 5 },
  { id: 3, text: "flowaer", amount: -5 },
]);

const total = computed(() => {
  return transactions.value.reduce((acc, item) => (acc += item.amount), 0);
});

//get income
</script>
