<script setup lang="ts">
import ShadowBox from './components/ShadowBox.vue'
</script>

<template>
  <main>
    <div class="max-w-sm mx-auto">
      <div class="grid grid-cols-3 gap-3 mx-auto my-3">
        <ShadowBox v-for="index in new Array(80)" :key="index" />
      </div>
      <div class="fixed left-0 top-0 w-full h-full flex justify-center items-center">
        <div class="text-3xl font-bold">LIGHT</div>
      </div>
    </div>
  </main>
</template>
