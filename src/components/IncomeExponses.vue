<script setup>
import { defineProps } from 'vue';


const props = defineProps({
    income: { type: Number, required: true },
    expense: { type: Number, required: true }
});

</script>

<template>
    <div class="inc-exp-container">
        <div>
            <h4>Доходы</h4>
            <p id="money-plus" class="money plus">+{{ income }} руб</p>
        </div>
        <div>
            <h4>Расходы</h4>
            <p id="money-minus" class="money minus">-{{ expense }} руб</p>
        </div>
    </div>
</template>

<style scoped></style>