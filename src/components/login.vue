<template>
  <div class="login-container">
    <div class="login-box">
      <div class="avatar-box">
        <img src="../assets/img/logo.png" alt>
      </div>
      <el-form :rules="rules" ref="loginFormRef" :model="loginForm">
        <el-form-item prop="username">
          <el-input v-model="loginForm.username">
            <i slot="prefix" class="iconfont icon-user"></i>
          </el-input>
        </el-form-item>
        <el-form-item prop="password">
          <el-input type="password" v-model="loginForm.password" @keyup.enter.native="login">
            <i slot="prefix" class="iconfont icon-3702mima"></i>
          </el-input>
        </el-form-item>
        <el-row>
          <el-col :offset="15">
            <el-button type="primary" @click="login">登录</el-button>
            <el-button type="info" @click="resForm">重置</el-button>
          </el-col>
        </el-row>
      </el-form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      loginForm: {
        username: '',
        password: ''
      },
      rules: {
        username: [
          { required: true, message: '请输入用户名', trigger: 'blur' }
        ],
        password: [{ required: true, message: '请输入密码', trigger: 'blur' }]
      }
    }
  },
  methods: {
    login() {
      this.$refs.loginFormRef.validate(async valid => {
        if (valid) {
          var { data: res } = await this.$http.post('/login', this.loginForm)
          console.log(res)
          if (res.meta.status !== 200) {
            this.$message.error('账号密码错误')
          }
          window.sessionStorage.setItem('token', res.data.token)
          this.$router.push('/home')
        }
      })
    },
    resForm() {
      this.$refs.loginFormRef.resetFields()
    }
  }
}
</script>

<style lang="less" scoped>
.login-container {
  background-color: #2b4b6b;
  height: 100%;
  overflow: hidden;
}
.login-box {
  width: 450px;
  height: 304px;
  border-radius: 4px;
  background-color: #ffff;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  .el-form {
    position: absolute;
    bottom: 0px;
    width: 100%;
    padding: 20px;
    box-sizing: border-box;
  }
}
.avatar-box {
  width: 130px;
  height: 130px;
  border: 1px solid #eee;
  border-radius: 50%;
  padding: 8px;
  box-shadow: 0 0 10px #eee;
  position: absolute;
  left: 50%;
  background-color: #ffff;
  transform: translate(-50%, -50%);
  img {
    width: 100%;
    height: 100%;
    background-color: #ffff;
    border-radius: 50%;
  }
}
</style>
