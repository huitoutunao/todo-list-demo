<template>
  <div class="my-dialog">
    <h1>{{ title }}</h1>
    <p>待修改的值：</p>
    <form action="." @submit.prevent="onSubmit">
      <input v-model="inputVal" type="text" placeholder="请输入修改任务名称" />
      <button type="submit">确认</button>
    </form>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const title = ref('提示')
const props = defineProps({
  editIndex: {
    type: Number,
    default: 0,
  },
})
const emit = defineEmits(['confirm'])

const inputVal = ref('')
const onSubmit = () => {
  emit('confirm', inputVal, props.editIndex)
}
</script>

<style lang="scss" scoped>
.my-dialog {
  position: relative;
}
</style>
