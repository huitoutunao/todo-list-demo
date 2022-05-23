<template>
  <div class="my-overlay">
    <h1>{{ title }}</h1>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const title = ref('遮罩层')
</script>

<style lang="scss" scoped>
.my-overlay {
  position: relative;
}
</style>
