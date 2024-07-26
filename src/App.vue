<script setup>
import Note from "/src/components/note.vue"
// 这部分写js, v3的话我目前只会简单的一点点  v2和v3有啥区别   写法不一样
// import {ref} from "vue"
// const msg = "123123"  // html部分要显示msg的值就要用到{{}}
// const num = ref(0)    // 使用ref是声明一个【响应式】的变量，可以在num的值改变之后，页面也会变化


//函数写法
const addBtn = () => {
  num.value++
}
</script>

<template>
  <!-- 注释快捷键  ctrl + / -->
  <!-- <div>{{ msg }}</div>
 
  <div>{{ num }}</div>
  <el-button type="primary" @click="addBtn">按钮</el-button> -->
 
  <Note />
</template>

<style scoped></style>
