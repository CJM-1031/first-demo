<template>
    <div class="task-manager">
      <h1>任务便签管理</h1>
      <div class="task-input">
        <!-- 输入框和添加按钮 -->
        <input type="text" v-model="newTask" placeholder="添加任务" />
        <button @click="addTask">添加</button>
      </div>
      <div class="task-search">
        <!-- 搜索框 -->
        <input type="text" v-model="searchQuery" placeholder="搜索任务" />
      </div>
      <ul class="task-list">
        <!-- 任务列表 -->
        <li v-for="(task, index) in filteredTasks" :key="index" :class="{ completed: task.completed }">
          <span @click="toggleTask(index)">
            <span v-html="highlightKeyword(task.content)"></span>
          </span>
          <button @click="editTask(index)">编辑</button>
          <button @click="deleteTask(index)">删除</button>
        </li>
      </ul>
      <div class="task-actions">
        <!-- 清除已完成任务按钮 -->
        <button @click="clearCompletedTasks">清除已完成任务</button>
      </div>
      <div class="task-summary">
        <!-- 任务统计 -->
        <p>已完成任务：{{ completedTasksCount }} 个</p>
        <p>未完成任务：{{ uncompletedTasksCount }} 个</p>
        <p>总任务数：{{ totalTasksCount }} 个</p>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, computed } from 'vue';
  
  // 任务列表
  const tasks = ref([
    { content: '学习 Vue', completed: false },
    { content: '写作业', completed: false },
    { content: '锻炼身体', completed: true },
    { content: '看书', completed: false },
    { content: '听音乐', completed: true },
    { content: '睡觉', completed: false },
  ]);
  
  // 新任务输入框绑定的变量
  const newTask = ref('');
  const searchQuery = ref('');
  const editIndex = ref(null);
  
  // 计算已完成任务数
  const completedTasksCount = computed(() => tasks.value.filter(task => task.completed).length);
  
  // 计算未完成任务数
  const uncompletedTasksCount = computed(() => tasks.value.filter(task => !task.completed).length);
  
  // 计算总任务数
  const totalTasksCount = computed(() => tasks.value.length);
  
  // 根据搜索关键字过滤任务列表
  const filteredTasks = computed(() => {
    if (!searchQuery.value) {
      return tasks.value;
    }
    return tasks.value.filter(task => task.content.toLowerCase().includes(searchQuery.value.toLowerCase()));
  });
  
  // 高亮显示搜索关键字
  function highlightKeyword(content) {
    if (!searchQuery.value) {
      return content;
    }
    const regex = new RegExp(`(${searchQuery.value})`, 'gi');
    return content.replace(regex, '<mark>$1</mark>');
  }
  
  // 添加新任务
  function addTask() {
    if (newTask.value.trim() !== '') {
      if (editIndex.value !== null) {
        tasks.value[editIndex.value].content = newTask.value;
        editIndex.value = null;
      } else {
        tasks.value.push({ content: newTask.value, completed: false });
      }
      newTask.value = ''; // 清空输入框
    }
  }
  
  // 切换任务完成状态
  function toggleTask(index) {
    tasks.value[index].completed = !tasks.value[index].completed;
  }
  
  // 编辑任务
  function editTask(index) {
    newTask.value = tasks.value[index].content;
    editIndex.value = index;
  }
  
  // 删除任务
  function deleteTask(index) {
    tasks.value.splice(index, 1);
  }
  
  // 清除已完成任务
  function clearCompletedTasks() {
    tasks.value = tasks.value.filter(task => !task.completed);
  }
  </script>
  
  <style scoped>
  .task-manager {
    max-width: 600px;
    margin: 0 auto;
    font-family: Arial, sans-serif;
  }
  
  .task-input, .task-search {
    display: flex;
    gap: 10px;
    margin-bottom: 20px;
  }
  
  .task-input input, .task-search input {
    flex: 1;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
  }
  
  .task-input button {
    padding: 10px 20px;
    border: none;
    background-color: #007bff;
    color: white;
    border-radius: 4px;
    cursor: pointer;
  }
  
  .task-input button:hover {
    background-color: #0056b3;
  }
  
  .task-list {
    list-style: none;
    padding: 0;
    margin: 0 0 20px 0;
    max-height: 400px; /* 设置最大高度 */
    overflow-y: auto;  /* 启用垂直滚动条 */
  }
  
  .task-list li {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
    margin-bottom: 10px;
    cursor: pointer;
  }
  
  .task-list li.completed span {
    text-decoration: line-through;
    color: #888;
  }
  
  .task-list button {
    background-color: #dc3545;
    color: white;
    border: none;
    padding: 5px 10px;
    border-radius: 4px;
    cursor: pointer;
  }
  
  .task-list button:hover {
    background-color: #c82333;
  }
  
  .task-actions {
    margin-bottom: 20px;
  }
  
  .task-actions button {
    padding: 10px 20px;
    border: none;
    background-color: #28a745;
    color: white;
    border-radius: 4px;
    cursor: pointer;
  }
  
  .task-actions button:hover {
    background-color: #218838;
  }
  
  .task-summary {
    text-align: center;
  }
  
  mark {
    background-color: yellow;
    padding: 0;
  }
  </style>
  