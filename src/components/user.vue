<template>
  <div>
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item :to="{ path: '/home' }">首页</el-breadcrumb-item>
      <el-breadcrumb-item>用户管理</el-breadcrumb-item>
      <el-breadcrumb-item>用户列表</el-breadcrumb-item>
    </el-breadcrumb>
    <el-card class="box-card">
      <el-input placeholder="请选择日期" v-model="userinput">
        <i slot="suffix" class="el-input__icon el-icon-search"></i>
      </el-input>
    </el-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      userinput: ''
    }
  }
}
</script>

<style lang="less" scoped>
el-input__inner {
  width: 285px;
  height: 40px;
}
</style>
