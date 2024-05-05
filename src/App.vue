<template>
  <Header />
  <div class="container">
    <Balance :total="total" />
    <IncomeExpenses :income="+income" :expenses="+expenses" />
    <TransactionList
      :transactions="transactions"
      @transactionDeleted="handleTransactionDeletion"
    />
    <AddTransaction @transactionSubmitted="handleTransactionSubmission" />
  </div>
</template>

<script setup>
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpenses from "./components/IncomeExpenses.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";

import { ref, computed, onMounted } from "vue";

const transactions = ref([]);

onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem("transactions"));
  if (savedTransactions) {
    transactions.value = savedTransactions;
  }
});
//Get total
const total = computed(() => {
  return transactions.value.reduce((acc, item) => (acc += item.amount), 0);
});

//Get income
const income = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
    .toFixed(2);
});

//Get expenses
const expenses = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
    .toFixed(2);
});

//Add transaction
function handleTransactionSubmission(transactionData) {
  const lastTransactionId =
    transactions.value.length > 0
      ? transactions.value[transactions.value.length - 1].id
      : 0;
  transactions.value.push({
    id: lastTransactionId + 1,
    text: transactionData.text,
    amount: transactionData.amount,
  });
  saveToLocalStorage();
}

//Delete transaction
function handleTransactionDeletion(id) {
  transactions.value = transactions.value.filter((tran) => {
    return tran.id !== id;
  });
  saveToLocalStorage();
}

//Save to local storage
function saveToLocalStorage() {
  localStorage.setItem("transactions", JSON.stringify(transactions.value));
}
</script>
