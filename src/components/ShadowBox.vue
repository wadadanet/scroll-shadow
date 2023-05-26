<template>
  <div class="box mx-auto" ref="boxRef" :style="{ boxShadow: boxShadow }"></div>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const boxRef = ref<HTMLElement | null>(null)
const shadowOffset = 5
const boxShadow = ref(`0px 0px ${shadowOffset}px rgba(0, 0, 0, 0.5)`)

onMounted(() => {
  window.addEventListener('resize', updateWindow)
  window.addEventListener('scroll', updateBoxShadow)
  updateWindow()
  updateBoxShadow()
})

onUnmounted(() => {
  window.removeEventListener('resize', updateWindow)
  window.removeEventListener('scroll', updateBoxShadow)
})

let windowWidth = window.innerWidth
let windowHeight = window.innerHeight

function updateWindow() {
  windowWidth = window.innerWidth
  windowHeight = window.innerHeight
}

function updateBoxShadow() {
  if (!boxRef.value) return

  const boxRect = boxRef.value.getBoundingClientRect()

  // Calculate the relative position of the box in the viewport (from -0.5 to 0.5)
  const relativePositionY = (boxRect.top + boxRect.height / 2) / windowHeight - 0.5
  const relativePositionX = (boxRect.left + boxRect.width / 2) / windowWidth - 0.5

  // Convert the relative position to a shadow offset (from -10px to 10px)
  const shadowOffsetY = relativePositionY * shadowOffset * 2
  const shadowOffsetX = relativePositionX * shadowOffset * 2

  // Create two shadows for the neumorphic effect
  const shadow1 = `${shadowOffsetX}px ${shadowOffsetY}px ${shadowOffset * 1.5}px rgba(0, 0, 0, 0.2)`
  const shadow2 = `${-shadowOffsetX}px ${-shadowOffsetY}px ${
    shadowOffset * 1.5
  }px rgba(255, 255, 255, 0.7)`

  boxShadow.value = `${shadow1}, ${shadow2}`
}
</script>
<style lang="postcss" scoped>
.box {
  @apply w-[50px] h-[50px] bg-gray-100 border-gray-100 rounded-3xl;
}
</style>
