<template>
    <h3>History</h3>
      <ul id="list" class="list" v-for="transaction in transactions">
        <li :class="{'minus': transaction.amount < 0, 'plus': transaction.amount >= 0}">
          {{transaction.text}} <span>${{transaction.amount}}</span>
          <button class="delete-btn" 
              @click="deleteTransaction(transaction.id)"> x
          </button>
        </li>
      </ul>
</template>

<script setup>
  import { defineProps,defineEmits } from 'vue';
  defineProps({
    transactions: Array
  })
  const emit=defineEmits(['delete-transaction'])
  const deleteTransaction=(id) => {
    emit('delete-transaction',id)
  }
  
</script>