<template>
  <div class="my-dialog">
    <h1>{{ title }}</h1>
    <p>待修改的值：</p>
    <input v-model="inputVal" type="text" placeholder="请输入修改任务名称" />
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'

const title = ref('提示')
const props = defineProps({
  editVal: {
    type: String,
    default: '',
  },
  editIndex: {
    type: Number,
    default: 0,
  },
})
const emit = defineEmits(['change'])

const inputVal = computed({
  get: () => {
    return props.editVal
  },
  set: (val) => {
    emit('change', val, props.editIndex)
  },
})
</script>

<style lang="scss" scoped>
.my-dialog {
  position: relative;
}
</style>
