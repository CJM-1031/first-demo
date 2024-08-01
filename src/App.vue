<script setup lang="ts">
import Note from "@/components/note.vue"
import HelloWorld from "@/components/HelloWorld.vue";
// 目前只能点击上面才能跳转，还是有点问题的
// 这部分写js, v3的话我目前只会简单的一点点  v2和v3有啥区别   写法不一样
// import {ref} from "vue"
// const msg = "123123"  // html部分要显示msg的值就要用到{{}}
// const num = ref(0)    // 使用ref是声明一个【响应式】的变量，可以在num的值改变之后，页面也会变化

//函数写法
//const addBtn = () => {
//  num.value++
//}
</script>

<template>
  <!-- 注释快捷键  ctrl + / -->
  <!-- <div>{{ msg }}</div>
 
  <div>{{ num }}</div>
  <el-button type="primary" @click="addBtn">按钮</el-button> -->
 
  <Note></Note>
  <HelloWorld></HelloWorld>
  <!-- 这个功能好了   就是鼠标移上去能看到element ui组件的文档 -->
  <!-- <el-table :data="data" style="width: 100%">
      <el-table-column prop="prop" label="label" width="width">
      </el-table-column>
  </el-table> -->
  <!-- 3、全局组件跳转
在工程项目中的vue文件、全局组件等外部组件都支持跳转。 -->
<!-- 就是上面这个全局组件跳转用不了 -->
  
</template>

<style scoped></style>
