<template>
  <div class="page">
    <div class="input-box">
      <input
        v-model="inputVal"
        type="text"
        placeholder="请输入任务名称"
        class="input"
        @keyup.enter="onConfirm"
      />
      <button class="confirm" @click="onConfirm">确认</button>
    </div>
    <ul class="list-box">
      <li v-for="(item, index) in todoList" :key="index" class="item">
        <input :id="item.id" type="checkbox" class="checkbox" />
        <label :for="item.id" class="label">{{ item.name }}</label>
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

interface todo {
  id: string
  name: string
}

const inputVal = ref<string>('')
const todoList = ref<todo[]>([])
const todoIndex = ref<number>(0)

const onConfirm = () => {
  todoList.value.push({
    id: `todo${todoIndex.value}`,
    name: inputVal.value,
  })

  inputVal.value = ''
  todoIndex.value += 1
}
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
}

ul li {
  list-style: none;
}

.page {
  position: relative;
  padding: 60px;

  .input-box {
    position: relative;
    height: 30px;
    padding-left: 15px;
    padding-right: 80px;
    line-height: 30px;
    border: 1px solid #d8d8d8;
    border-radius: 8px;
    overflow: hidden;

    .input {
      width: 100%;
      height: 100%;
      font-size: 16px;
      color: #333;
      border: none;
      outline: none;
    }

    input::-webkit-input-placeholder {
      color: #999;
    }

    .confirm {
      position: absolute;
      top: 0;
      right: 0;
      height: 100%;
      padding: 0 20px;
      font-size: 14px;
      color: #fff;
      background: #8888f8;
      border: none;
    }
  }

  .list-box {
    padding: 15px 10px;

    .item {
      display: flex;
      align-items: center;
      padding: 5px 0;
      font-size: 18px;
      color: #333;
    }

    .checkbox {
      width: 18px;
      height: 18px;
    }

    .label {
      flex: 1;
      padding-left: 5px;
      overflow: hidden;
    }
  }
}
</style>
