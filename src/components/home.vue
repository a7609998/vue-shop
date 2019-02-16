<template>
  <el-container>
    <el-header>
      <div class="logobox">
        <img src="../assets/img/homelogo.png" alt>
        <span>电商后台管理系统</span>
      </div>
      <el-button type="info" @click="logout">退出</el-button>
    </el-header>
    <el-container>
      <el-aside :width="menushow ? '65px':'200px'">
        <div class="muesss" @click="menushow=!menushow">|||</div>
        <el-menu
          background-color="#333744"
          text-color="#fff"
          active-text-color="#409EFF"
          :unique-opened="true"
          :style="menushow ? 'width=65px':'width=200px'"
          :collapse="menushow"
          :collapse-transition="false"
          :router="true"
        >
          <el-submenu :index="item.id+''" v-for="(item,k) in menulist" :key="item.id">
            <template slot="title">
              <i :class="'iconfont icon-' + menuicon[k]"></i>
              <span>{{item.authName}}</span>
            </template>
            <el-menu-item
              v-for="item2 in item.children"
              :key="item2.id"
              :index="item2.path"
            >
              <i class="el-icon-menu"></i>
              {{item2.authName}}
            </el-menu-item>
          </el-submenu>
        </el-menu>
      </el-aside>
      <el-main>
        <router-view/>
      </el-main>
    </el-container>
  </el-container>
</template>

<script>
export default {
  created() {
    this.gethomeuser()
  },
  data() {
    return {
      menushow: false,
      menulist: [],
      menuicon: ['users', 'tijikongjian', 'shangpin', 'danju', 'baobiao']
    }
  },
  methods: {
    async gethomeuser() {
      var { data: res } = await this.$http.get('/menus')
      console.log(res)
      if (res.meta.status === 200) {
        this.menulist = res.data
      }
    },
    logout() {
      this.$confirm('确定要退出系统吗', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      })
        .then(() => {
          window.sessionStorage.removeItem('token')
          this.$router.push('/login')
        })
        .catch(() => {})
    }
  }
}
</script>

<style lang="less" scoped>
.el-container {
  height: 100%;
  .el-header {
    background-color: #373d41;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0;
    padding-right: 20px;
    height: 60px;
    .logobox {
      display: flex;
      color: #fff;
      font-size: 22px;
      align-items: center;
      user-select: none;
      img {
        width: 50px;
        height: 50px;
        margin-right: 10px;
      }
    }
  }

  .el-aside {
    background-color: #333744;
    .muesss {
      background: rgb(74, 80, 100);
      color: #fff;
      height: 25px;
      line-height: 25px;
      font-size: 12px;
      text-align: center;
      letter-spacing: 0.1em;
      user-select: none;
      cursor: pointer;
    }
    .el-row {
      .el-menu {
        border: none;
      }
    }
  }

  .el-main {
    background-color: #eaedf1;
  }
}
</style>
