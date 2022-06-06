<template>
  <div class="my-overlay animate__animated animate__fadeIn">
    <!--  -->
  </div>
</template>

<script setup lang="ts">
import { onMounted } from 'vue'

onMounted(() => {
  //
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
