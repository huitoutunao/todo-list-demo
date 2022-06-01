<template>
  <div class="page">
    <div class="input-box">
      <input
        v-model="inputVal"
        type="text"
        placeholder="请输入任务名称"
        :class="['input', placeholderStyle ? 'active' : 'inactive']"
        @keyup.enter="onConfirm"
      />
      <button class="confirm" @click="onConfirm">确认</button>
    </div>
    <ul class="list-box">
      <li v-for="(item, index) in todoList" :key="index" class="item">
        <div class="check-box">
          <input :id="item.id" v-model="item.checked" type="checkbox" class="checkbox" />
          <label :for="item.id" :class="['label', { checked: item.checked }]">
            <span class="word">{{ item.text }}</span>
          </label>
        </div>
        <button class="action-btn" @click="onEdit(index)">
          <i class="iconfont iconbianji"></i>
        </button>
        <button class="action-btn" @click="onDel(index)">
          <i class="iconfont iconshanchu"></i>
        </button>
      </li>
    </ul>
    <MyDialog v-show="isShowDialog" :edit-index="editIndex" @confirm="confirmDialogVal"></MyDialog>
  </div>
</template>

<script setup lang="ts">
import { ref, Ref, unref, reactive, watchEffect } from 'vue'
import MyDialog from '@/components/my-dialog/Index.vue'

interface todo {
  id: string
  text: string
  checked: boolean
}

const inputVal = ref<string>('')
const todoList = reactive<todo[]>([])
const todoIndex = ref<number>(0)
const placeholderStyle = ref<boolean>(false)

watchEffect(() => {
  if (inputVal.value) {
    placeholderStyle.value = false
  }
})

const onConfirm = () => {
  if (!inputVal.value) {
    placeholderStyle.value = true
    return
  }

  todoList.push({
    id: `todo${todoIndex.value}`,
    text: inputVal.value,
    checked: false,
  })

  inputVal.value = ''
  todoIndex.value += 1
}

const editIndex = ref<number>(0)
const isShowDialog = ref<boolean>(false)
const onEdit = (index: number) => {
  editIndex.value = index
  isShowDialog.value = true
}

const confirmDialogVal = (v: string | Ref<string>, index: number) => {
  if (unref(v)) {
    todoList[index].text = unref(v)
  }
  isShowDialog.value = false
}

const onDel = (index: number) => {
  todoList.splice(index, 1)
}
</script>

<style lang="scss">
@import '@/assets/font/iconfont.css';

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

      &.inactive::-webkit-input-placeholder {
        color: #999;
      }

      &.active::-webkit-input-placeholder {
        color: #ff0000;
      }
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
      cursor: pointer;
    }
  }

  .list-box {
    padding: 15px 10px;

    .item {
      position: relative;
      display: flex;
      align-items: center;
      padding: 10px 0;
      font-size: 18px;
      color: #333;
      border-bottom: 1px solid #eee;

      &:hover {
        .action-btn {
          opacity: 1;
          visibility: visible;
        }
      }
    }

    .check-box {
      position: relative;
      display: flex;
      align-items: center;
      flex: 1;
      overflow: hidden;

      .checkbox {
        position: absolute;
        clip: rect(0, 0, 0, 0);

        &:checked + label::before {
          color: #8888f8;
        }
      }

      .label {
        display: flex;
        align-items: center;
        width: 100%;

        &::before {
          content: '\e647';
          display: block;
          padding-left: 5px;
          padding-right: 10px;
          font-family: 'iconfont';
          font-size: 24px;
          color: #eee;
          transition: all 0.2s ease;
        }

        &.checked .word {
          color: #d8d8d8;
          text-decoration: line-through;
        }

        .word {
          color: #333;
          transition: all 0.2s ease;
        }
      }
    }

    .action-btn {
      padding: 5px 15px;
      font-size: 12px;
      color: red;
      background: #fff;
      border: none;
      opacity: 0;
      visibility: hidden;
      transition: all 0.2s ease;

      .iconbianji {
        color: #3636f0;
        font-size: 22px;
      }

      .iconshanchu {
        color: red;
        font-size: 20px;
      }
    }
  }
}
</style>
