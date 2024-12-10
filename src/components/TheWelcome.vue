<script setup lang="ts">
import { useRouter } from 'vue-router';
const router = useRouter();
function gotoOrder() {
  router.push('/orders');
}
</script>

<template>
  <div class="flex flex-col justify-center items-center pt-20">
    <div class="pb-10">
      <h1 class="text-4xl font-bold text-green-700 text-center">Gollachhut admin panel</h1>
      <p class="text-green-700 pt-3">Currently we only have orders options</p>
    </div>
    <div>
      <ul class="flex space-x-4">
        <li class="p-4 bg-green-700 text-white rounded-md hover:scale-110 transition-all" @click="gotoOrder">
          Orders
        </li>
      </ul>
    </div>
  </div>
</template>
