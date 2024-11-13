<script setup>
import { computed, ref,onMounted } from 'vue';
import '../style.css'
import AddTransaction from './components/Add Transaction.vue';
import Balance from './components/Balance.vue';
import Header from './components/Header.vue'
import IncomeExpense from './components/IncomeExpense.vue';
import TransactionsList from './components/TransactionsList.vue';

const transactions=ref([]);
  onMounted(() => {
    const savedTransactions=JSON.parse(localStorage.getItem('transactions'))
    if(savedTransactions) transactions.value=savedTransactions
  })

  const expense= computed(() => {
    return transactions.value.filter(t => t.amount<0).reduce((sum,t)=>sum+t.amount,0)
  })
  const income= computed(() => {
    return transactions.value.filter(t => t.amount>0).reduce((sum,t)=>sum+t.amount,0)
  })
  const balance= computed(() => {
    return income.value+expense.value
  })

  const handleAddTransaction=((newTransaction) => {
    transactions.value.push(newTransaction)
    saveTransactionsToLocalStorage()
  })

  const handleDeleteTransaction=(id) => {
    transactions.value=transactions.value.filter(t => t.id!==id)
    saveTransactionsToLocalStorage()
  }
  const saveTransactionsToLocalStorage=() => {
    localStorage.setItem('transactions',JSON.stringify(transactions.value))
  }


</script>

<template>
  <div class="container">
    <Header/>
    <Balance  :balance="+balance"/>
    <IncomeExpense  :income="+income" :expense="+expense"/>
    <TransactionsList :transactions="transactions" 
    @delete-transaction="handleDeleteTransaction"/>
    <AddTransaction @add-transaction="handleAddTransaction" />

  </div>
  
</template>

