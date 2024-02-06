<script setup>
import { defineProps } from "vue";

const props = defineProps({
  transactions: Array,
  required: true,
});

const emits = defineEmits(["transactionDelete"]);

const deleteTransaction = (id) => {
  emits("transactionDelete", id);
};
</script>

<template>
  <div>
    <h3>История</h3>
    <ul
      id="list"
      class="list"
      v-for="transaction in transactions"
      :key="transaction.id"
    >
      <li :class="transaction.amount < 0 ? 'minus' : 'plus'">
        {{ transaction.text }} <span>{{ transaction.amount }} руб</span>
        <button @click="deleteTransaction(transaction.id)" class="delete-btn">
          x
        </button>
      </li>
    </ul>
  </div>
</template>

<style scoped></style>
