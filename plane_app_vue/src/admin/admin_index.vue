<template>
<div>
  <el-tabs v-model="activeName" type="card" @tab-click="handleClick">
    <el-tab-pane label="首页" name="first">首页</el-tab-pane>
    <el-tab-pane label="用户管理" name="second">
      <user></user>
    </el-tab-pane>
    <el-tab-pane label="配置管理" name="third">配置管理</el-tab-pane>
    <el-tab-pane label="角色管理" name="fourth">角色管理</el-tab-pane>
    <el-tab-pane label="定时任务补偿" name="fifth">定时任务补偿</el-tab-pane>
  </el-tabs>
</div>
</template>
<script>
import user from './children/user.vue';
  export default {
    
    data() {
      return {
        activeName: 'first'
      };
    },
    methods: {
      handleClick(tab, event) {
        console.log(tab, event);
      }
    },
    components:{
      user,
    }
  };
</script>