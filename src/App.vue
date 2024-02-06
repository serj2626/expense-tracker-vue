<script setup>
import { ref, computed, onMounted } from "vue";
import { useToast } from "vue-toastification";
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpenses from "./components/IncomeExponses.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";

const transactions = ref([]);

onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem("transactions"));

  if (savedTransactions) {
    transactions.value = savedTransactions;
  }
});

//get total
const total = computed(() => {
  let balance = 0;
  transactions.value.forEach((element) => {
    balance += element.amount;
  });
  return balance;
});

//get income
const income = computed(() => {
  let total_income = 0;
  transactions.value.forEach((element) => {
    element.amount > 0 ? (total_income += element.amount) : "";
  });
  return +total_income.toFixed(2);
});

//get expense
const expense = computed(() => {
  let total_expense = 0;
  transactions.value.forEach((element) => {
    element.amount < 0 ? (total_expense += Math.abs(element.amount)) : "";
  });
  return +total_expense.toFixed(2);
});
const toast = useToast();
const handleTransactionDeleted = (id) => {
  transactions.value = transactions.value.filter(
    (transaction) => transaction.id !== id
  );
  toast.success("Транзакция удалена");
};


const saveTransactionsToLocalStorage = () => {
  localStorage.setItem("transactions", JSON.stringify(transactions.value));
};
</script>

<template>
  <div>
    <Header />
  </div>
  <div class="container">
    <Balance :total="total" />
    <IncomeExpenses :income="income" :expense="expense" />
    <TransactionList
      @transactionDelete="handleTransactionDeleted"
      :transactions="transactions"
    />
    <AddTransaction @addTransaction="transactions.push($event)" />
  </div>
</template>

<style scoped></style>
