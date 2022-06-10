<template>
  <div v-show="show" class="my-dialog">
    <div
      :class="[
        'dialog-content animate__animated',
        show ? 'animate__zoomIn animate__faster' : 'animate__zoomOut animate__faster',
      ]"
    >
      <div class="dialog-title">{{ title }}</div>
      <div class="dialog-input">
        <input v-model="inputVal" type="text" placeholder="请编辑任务名称" class="input" />
      </div>
      <button class="dialog-confirm" @click="onSubmit">确认</button>
    </div>
    <MyOverlay :show-overlay="show" @click="closeOverlay"></MyOverlay>
  </div>
</template>

<script setup lang="ts">
import { ref, watch } from 'vue'
import MyOverlay from '@/components/my-overlay/Index.vue'

const title = ref('提示')
const props = defineProps({
  show: {
    type: Boolean,
    default: false,
  },

  editIndex: {
    type: Number,
    default: 0,
  },
})
const emit = defineEmits(['confirm', 'closeOverlay'])

const inputVal = ref<string>('')
const onSubmit = () => {
  emit('confirm', inputVal, props.editIndex)
}

watch(
  () => props.show,
  (nVal) => {
    if (nVal) {
      inputVal.value = ''
    }
  }
)

const closeOverlay = () => {
  emit('closeOverlay', !props.show)
}
</script>

<style lang="scss" scoped>
.my-dialog {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 9;

  .dialog-content {
    position: absolute;
    top: 50%;
    left: 50%;
    z-index: 2002;
    width: 300px;
    margin-top: -70px;
    margin-left: -150px;
    padding: 15px;
    background-color: #fff;
    border-radius: 10px;
    box-sizing: border-box;

    .dialog-title {
      line-height: 30px;
      text-align: center;
      font-size: 18px;
    }

    .dialog-input {
      height: 40px;
      margin-bottom: 30px;
      border-bottom: 1px solid #eee;

      .input {
        width: 100%;
        height: 100%;
        line-height: 45px;
        font-size: 14px;
        color: #666;
        border: none;
        outline: none;
      }
    }

    .dialog-confirm {
      width: 100%;
      height: 40px;
      line-height: 40px;
      text-align: center;
      font-size: 16px;
      color: #fff;
      background-color: #6f6ff8;
      border-radius: 20px;
      border: none;
    }
  }
}
</style>
