<script setup lang="ts">
import { ref } from 'vue';
import TheWelcome from '../components/TheWelcome.vue';

const postData = async () => {
  const options = {
    method: 'POST',
    headers: {
      Accept: 'application/json',
      'RT-UDDOKTAPAY-API-KEY': '982d381360a69d419689740d9f2e26ce36fb7a50',
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({
      full_name: 'John Doe',
      email: 'userEmail@gmail.com',
      amount: '100',
      metadata: { user_id: '10', order_id: '50' },
      redirect_url: 'https://your-domain.com/success',
      cancel_url: 'https://your-domain.com/cancel',
      webhook_url: 'https://your-domain.com/ipn'
    })
  };

  try {
    const response = await fetch('https://sandbox.uddoktapay.com/api/checkout-v2', options);
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error(error);
  }
};
</script>

<template>
  <main>
    <TheWelcome />
    <button @click="postData">Submit Payment</button>
  </main>
</template>
