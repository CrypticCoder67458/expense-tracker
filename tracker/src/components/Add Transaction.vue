<template>
    <h3>Add new transaction</h3>
      <form id="form"  @submit.prevent="handleSubmit" >
        <div class="form-control">
          <label for="text">Text</label>
          <input type="text" id="text" v-model="text" placeholder="Enter text..." />
        </div>
        <div class="form-control">
          <label for="amount"
            >Amount <br />
            (negative - expense, positive - income)</label
          >
          <input type="number" id="amount"  v-model="amount" placeholder="Enter amount..." />
        </div>
        <button class="btn" type="submit" >Add transaction</button>
      </form>
</template>


<script setup>
import { ref, defineEmits } from 'vue';
const amount=ref(0)
const text=ref('')
const emit=defineEmits(['add-transaction'])

const handleSubmit = () => {
  
  if(!text.value || !amount.value){
    return
  } 
  const newTransaction = {
    id: Math.floor(Math.random() * 100000000),
    text: text.value,
    amount: +amount.value
  }
  console.log('submitted')
  emit('add-transaction', newTransaction)
  text.value=''
  amount.value=0
}
</script>