<template>
  <div id="app">
    <el-container>
      <!-- 顶部导航栏 -->

      <div class="j-header">
        <el-row :gutter="4">
          <el-col :span="1">
            <div class="grid-content"></div>
          </el-col>

          <!-- logo -->
          <el-col :span="4">
            <router-link to="/">
              <div class="logo">
                <img src="./assets/img/logo.png" alt="logo" />
              </div>
            </router-link>
          </el-col>
          <!-- logo END -->

          <!-- menu -->
          <el-col :span="17">
            <el-menu
              :default-active="activeIndex2"
              class="el-menu-demo"
              mode="horizontal"
              @select="handleSelect"
              background-color="#545c64"
              text-color="#fff"
              active-text-color="#ffd04b"
            >
              <el-menu-item index="1">未完成代办</el-menu-item>
              <el-menu-item index="2">已完成代办</el-menu-item>
              <el-menu-item index="3">我的消息</el-menu-item>
              <el-menu-item index="4">设置</el-menu-item>
            </el-menu>
          </el-col>
          <!-- menu END -->

          <!-- userAvatar -->
          <el-col :span="2" style="height: 60px">
            <div class="j-avatar">
              <el-avatar
                shape="square"
                size="medium"
                fit="fill"
                :src="avatarUrl"
                @error="avatarErrorHandler"
              ></el-avatar>
            </div>
          </el-col>
          <!-- userAvatar END -->
        </el-row>
      </div>

      <!-- 顶部导航栏END -->

      <el-main class="j-main">
        <MyTodoList></MyTodoList>
      </el-main>

      <!-- 底栏容器 -->
      <el-footer style="padding: 0px">
        <div class="j-footer">
          <div class="github">
            <div class="github-but"></div>
          </div>
          <div class="j-footer-help">
            <p>
              <a href="http://github.com/ErizJ">隐私政策</a>
              <span>|</span>
              <a href="http://github.com/ErizJ">使用条款</a>
              <span>|</span>
              <a href="http://github.com/ErizJ">法律信息</a>
            </p>
            <p class="coty">Copyright &copy; 2022 Jtodos Inc. 保留所有权利</p>
            <p class="coty">Power By ErizJ</p>
          </div>
        </div>
      </el-footer>
    </el-container>
  </div>
</template>

<script>
import MyTodoList from './components/MyTodoList.vue'

export default {
  name: 'App',
  components: {
    MyTodoList,
  },
  data() {
    return {
      //导航栏菜单相关
      activeIndex: '1',
      activeIndex2: '1',

      //用户相关
      avatarUrl:
        'https://cube.elemecdn.com/0/88/03b0d39583f48206768a7534e55bcpng.png',
    }
  },
  methods: {
    //菜单选择回调
    handleSelect(key, keyPath) {
      console.log(key, keyPath)
    },

    //用户头像获取失败回调
    avatarErrorHandler() {
      this.avatarUrl =
        'https://cube.elemecdn.com/e/fd/0fc7d20532fdaf769a25683617711png.png'
      return true
    },
  },
}
</script>

<style lang="css">
@import './reset.css';

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #fff;
  margin-top: 60px;
}

html {
  font-family: 'Helvetica Neue', Helvetica, 'PingFang SC', 'Hiragino Sans GB',
    'Microsoft YaHei', '微软雅黑', Arial, sans-serif;
  background-color: #545c64;
  min-width: 600px;
  /* overflow-x: hidden; */
}
/* 全局CSS */

#app .el-main {
  height: auto;
  width: auto;
}

a,
a:hover {
  text-decoration: none;
}

.grid-content {
  min-height: 60px;
  background-color: transparent;
}
/* 全局CSS END */

/* 顶部导航栏CSS */
.j-header {
  background-color: transparent;
  width: 100%;
  height: 60px;
  position: fixed;
  top: 0;
  z-index: 9999;
  border-bottom: 1px solid rgb(230, 230, 230);
}

.j-userBar {
  height: 60px;
  background-color: #fff;
  float: right;
}

.j-userAvatar {
  height: 100%;
  padding: 10px 0px;
  background-color: transparent;
}

.j-avatar {
  height: 100%;
}
.j-avatar el-avatar {
  height: 100%;
  display: block;
}

.logo {
  display: flex;
  width: 190px;
}

.logo img {
  display: flex;
  width: 100%;
}

/* 顶部导航栏CSS END */

/* 底栏容器CSS */
.j-footer {
  width: 100%;
  height: auto;
  text-align: center;
  background-color: transparent;
  padding-bottom: 20px;
  border-top: 1px solid #fff;
}

.j-footer .github {
  height: 60px;
  line-height: 60px;
  margin-top: 20px;
}
.j-footer .github .github-but {
  width: 190px;
  text-align: center;
  height: 60px;
  margin: 0 auto;
  background: url('./assets/img/logo.png') no-repeat;
}
.j-footer .j-footer-help {
  text-align: center;
  color: #fff;
}
.j-footer .j-footer-help p {
  margin: 20px 0 16px 0;
}

.j-footer .j-footer-help p a {
  color: #fff;
  text-decoration: none;
}
.j-footer .j-footer-help p a:hover {
  color: #fff;
}
.j-footer .j-footer-help p span {
  padding: 0 22px;
}
/* 底栏容器CSS END */
</style>
