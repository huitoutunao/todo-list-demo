<template>
  <div class="my-dialog">
    <div class="dialog-content">
      <h1>{{ title }}</h1>
      <p>待修改的值：</p>
      <form action="." @submit.prevent="onSubmit">
        <input v-model="inputVal" type="text" placeholder="请输入修改任务名称" />
        <button type="submit">确认</button>
      </form>
    </div>
    <MyOverlay></MyOverlay>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import MyOverlay from '@/components/my-overlay/Index.vue'

const title = ref('提示')
const props = defineProps({
  editIndex: {
    type: Number,
    default: 0,
  },
})
const emit = defineEmits(['confirm'])

const inputVal = ref<string>('')
const onSubmit = () => {
  emit('confirm', inputVal, props.editIndex)
}
</script>

<style lang="scss" scoped>
.my-dialog {
  position: relative;

  .dialog-content {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    padding: 30px;
    background-color: #fff;
    border-radius: 10px;
    z-index: 9;
  }
}
</style>
