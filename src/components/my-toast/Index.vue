<template>
  <div class="my-toast">
    <h1>{{ title }}</h1>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const title = ref('轻提示')
</script>

<style lang="scss" scoped>
.my-toast {
  position: relative;
}
</style>
