<script setup>
import { ref } from "vue";
import { useToast } from "vue-toastification";



const toast = useToast();

const text = ref("");
const amount = ref('');

const emits = defineEmits(['addTransaction']);

const onSubmit = () => {
    if (!text.value || !amount.value) {
        toast.error('Поля не должны быть пустыми');
        return
    }
    const newTransaction = {
        id: Math.random(),
        text: text.value,
        amount: parseFloat(amount.value)
    }
    emits('addTransaction', newTransaction);
    text.value = '';
    amount.value = '';

};
</script>

<template>
    <h3>Добавить новую транзакцию</h3>
    <form id="form" @submit.prevent="onSubmit">

        <div class="form-control">
            <label for="text">Текст</label>
            <input v-model="text" type="text" id="text" placeholder="Введите текст..." />
        </div>


        <div class="form-control">
            <label for="amount">Сумма <br />
                (минус - расходы, плюс - доходы)</label>
            <input v-model="amount" type="number" id="amount" placeholder="Введите сумму..." />
        </div>


        <button class="btn">Добавить</button>
    </form>
</template>

<style scoped></style>
