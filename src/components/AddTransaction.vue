<template>
  <h3>Add new transaction</h3>
  <form id="form" @submit.prevent="onSubmit">
    <div class="form-control">
      <label for="text">Text</label>
      <input type="text" id="text" placeholder="Enter text..." v-model="text" />
    </div>
    <div class="form-control">
      <label for="amount"
        >Amount <br />
        (- Red, + Green)</label
      >
      <input
        type="text"
        id="amount"
        placeholder="Enter amount..."
        v-model="amount"
      />
    </div>
    <button class="btn">Add transaction</button>
  </form>
</template>

<script setup>
import { ref } from "vue";
import { createToastInterface, useToast } from "vue-toastification";
const emit = defineEmits(["transactionSubmitted"]);
const toast = useToast();

function onSubmit() {
  if (isNaN(amount.value)) {
    toast.error("Amount must be a number!");
    return;
  }
  if (!text.value || !amount.value) {
    toast.error("Both values must be filled!");
  } else {
    toast.success("ezpz noob");
    const transactionData = {
      text: text.value,
      amount: +amount.value,
    };
    emit("transactionSubmitted", transactionData);
  }
  console.log(text.value, amount.value);
}

const text = ref("");
const amount = ref("");
</script>
