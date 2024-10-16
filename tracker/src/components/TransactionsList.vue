<template>
    <h3>History</h3>
      <ul id="list" class="list" v-for="transaction in transactions">
        <li :class="{'minus': transaction.amount < 0, 'plus': transaction.amount >= 0}">
          {{transaction.text}} <span>${{transaction.amount}}</span><button class="delete-btn">x</button>
        </li>
      </ul>
</template>

<script setup>
  import { defineProps } from 'vue';
  defineProps({
    transactions: Array
  })
  
</script>