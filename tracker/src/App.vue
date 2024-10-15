<script setup>
import { ref } from 'vue';
import '../style.css'
import AddTransaction from './components/Add Transaction.vue';
import Balance from './components/Balance.vue';
import Header from './components/Header.vue'
import IncomeExpense from './components/IncomeExpense.vue';
import TransactionsList from './components/TransactionsList.vue';

const income=ref (0);
const expense=ref(0);
const transactions=ref([]);

</script>

<template>
  <div class="container">
    <Header />
    <Balance />
    <IncomeExpense />
    <TransactionsList />
    <AddTransaction />

  </div>
  
</template>

