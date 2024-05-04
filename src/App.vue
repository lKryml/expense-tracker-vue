<template>
  <Header />
  <div class="container">
    <Balance />
    <IncomeExpenses />
    <TransactionList :transactions="transactions"  />
    <AddTransaction />
  </div>
</template>

<script setup>
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpenses from "./components/IncomeExpenses.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";
import computed from "vue";
const transactions = [
  { id: 1, text: "flower", amount: 100 },
  { id: 2, text: "floweer", amount: 200 },
  { id: 3, text: "flowaer", amount: -300 },
];

</script>
