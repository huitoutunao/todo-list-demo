<template>
  <div class="my-overlay">
    <!--  -->
  </div>
</template>

<script setup lang="ts">
import { onMounted } from 'vue'

onMounted(() => {
  // 遮罩层
})
</script>

<style lang="scss" scoped>
.my-overlay {
  position: fixed;
  top: 0;
  left: 0;
  z-index: 1;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.7);
}
</style>
