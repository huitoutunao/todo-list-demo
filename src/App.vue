<template>
  <div class="page">
    <div class="input-box">
      <input type="text" placeholder="请输入任务名称" class="input" />
    </div>
    <ul class="list-box">
      <li class="item">
        <input id="todo1" type="checkbox" class="checkbox" />
        <label for="todo1" class="label">吃饭</label>
      </li>
      <li class="item">
        <input id="todo2" type="checkbox" class="checkbox" />
        <label for="todo2" class="label">洗澡</label>
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
// import { ref, reactive } from 'vue'

// const inputVal = ref<string>('')
// const todoList = reactive([])

// console.log(todoList)
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
    height: 30px;
    padding: 0 15px;
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
