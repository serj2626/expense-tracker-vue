<script setup>
import { defineProps } from 'vue';

const props = defineProps({
    total: Number, required: true
});
</script>

<template>
    <div>
        <h4>Твой баланс</h4>
        <h1 id="balance">{{ total }} руб</h1>
    </div>
</template>


<style scoped></style>