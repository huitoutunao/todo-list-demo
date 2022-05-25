<template>
  <div class="my-dialog">
    <h1>{{ title }}</h1>
    <p>待修改的值：{{ editVal }}</p>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

console.log('传入值')
const title = ref('提示')
const editVal = ref('')
</script>

<style lang="scss" scoped>
.my-dialog {
  position: relative;
}
</style>
