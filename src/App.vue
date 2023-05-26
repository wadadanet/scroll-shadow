<script setup lang="ts">
import ShadowBox from './components/ShadowBox.vue'
</script>

<template>
  <main>
    <div class="container my-6 relative">
      <div class="grid grid-cols-5 gap-6">
        <ShadowBox v-for="index in new Array(60)" :key="index" />
      </div>
      <div class="fixed left-0 top-0 w-full h-full flex justify-center items-center">
        <div class="text-3xl font-bold">LIGHT</div>
      </div>
    </div>
  </main>
</template>
