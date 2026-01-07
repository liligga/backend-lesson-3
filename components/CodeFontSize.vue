<script setup lang="ts">
import { watch, onMounted } from 'vue'
import { fontSize, MIN_SIZE, MAX_SIZE, STEP } from '../composables/useCodeFontSize'

// Apply font size to global CSS variable
function applyFontSize() {
  document.documentElement.style.setProperty(
    '--slidev-code-font-size',
    `${fontSize.value}px`
  )
}

// Watch for changes and apply immediately
watch(fontSize, applyFontSize, { immediate: true })

// Initialize on mount (ensures CSS variable is set)
onMounted(() => {
  applyFontSize()
})

// Increment/decrement functions
function increase() {
  if (fontSize.value < MAX_SIZE) {
    fontSize.value += STEP
  }
}

function decrease() {
  if (fontSize.value > MIN_SIZE) {
    fontSize.value -= STEP
  }
}
</script>

<template>
  <div class="code-font-size-overlay">
    <div
      flex="~ gap-2 items-center"
      border="~ main rounded-md"
      p="2"
      bg="white dark:gray-800"
      text="xs"
      class="control-panel"
    >
      <button
        @click="decrease"
        :disabled="fontSize <= MIN_SIZE"
        :aria-disabled="fontSize <= MIN_SIZE"
        p="1"
        px="2"
        border="~ main rounded"
        bg="blue-600 disabled:gray-300"
        text="white disabled:gray-600"
        hover:bg="blue-700"
        title="Decrease font size"
      >
        −
      </button>

      <span text="sm" min-w="60px" text-center>
        {{ fontSize }}px
      </span>

      <button
        @click="increase"
        :disabled="fontSize >= MAX_SIZE"
        :aria-disabled="fontSize >= MAX_SIZE"
        p="1"
        px="2"
        border="~ main rounded"
        bg="blue-600 disabled:gray-300"
        text="white disabled:gray-600"
        hover:bg="blue-700"
        title="Increase font size"
      >
        +
      </button>
    </div>
  </div>
</template>

<style scoped>
.code-font-size-overlay {
  position: fixed;
  top: 1rem;
  right: 1rem;
  z-index: 100;
}

.control-panel {
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
  backdrop-filter: blur(8px);
  background-color: rgba(255, 255, 255, 0.95);
}

.dark .control-panel {
  background-color: rgba(31, 41, 55, 0.95);
}

.control-panel:hover {
  box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
}
</style>
