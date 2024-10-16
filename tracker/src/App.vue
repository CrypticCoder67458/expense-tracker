<script setup>
import { computed, ref } from 'vue';
import '../style.css'
import AddTransaction from './components/Add Transaction.vue';
import Balance from './components/Balance.vue';
import Header from './components/Header.vue'
import IncomeExpense from './components/IncomeExpense.vue';
import TransactionsList from './components/TransactionsList.vue';

const transactions=ref([
  {id:1, text:'Flower', amount:-20},
  {id:2, text:'Salary', amount:300},
  {id:3, text:'Book', amount:-10},
  {id:4, text:'Camera', amount:-50}
  ]);

  const expense= computed(() => {
    return transactions.value.filter(t => t.amount<0).reduce((sum,t)=>sum+t.amount,0)
  })
  const income= computed(() => {
    return transactions.value.filter(t => t.amount>0).reduce((sum,t)=>sum+t.amount,0)
  })
  const balance= computed(() => {
    return income.value+expense.value
  })


</script>

<template>
  <div class="container">
    <Header />
    <Balance  :balance="balance"/>
    <IncomeExpense  :income="income" :expense="expense"/>
    <TransactionsList :transactions="transactions" />
    <AddTransaction />

  </div>
  
</template>

