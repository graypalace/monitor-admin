<template>
  <div class="layout">
    <el-container v-if="showMenu" class="container">
      <el-aside class="aside">
        <div class="head">
          <div>
            <img src="//s.weituibao.com/1582958061265/mlogo.png" alt="logo">
            <span>Monitor-plus</span>
          </div>
        </div>
        <div class="line" />
        <el-menu
            active-text-color="#ffd04b"
            background-color="#222832"
            text-color="#fff"
            :router="true"
            :default-openeds="defaultOpen"
            :default-active='currentPath'
            @open="handleOpen"
            @close="handleClose"
            default-active="2"
        >
          <el-sub-menu index="1">
            <template #title>
              <span>仪表盘(Dashboard)</span>
            </template>
            <el-menu-item-group>
              <el-menu-item index="/"><i class="el-icon-odometer" />汇总展示</el-menu-item>
              <el-menu-item index="/showView"><i class="el-icon-plus" />大屏展示</el-menu-item>
            </el-menu-item-group>
          </el-sub-menu>
          <el-sub-menu index="2">
            <template #title>
              <span>资源管理</span>
            </template>
            <el-sub-menu index="2-1">
              <template #title>资源信息</template>
              <el-menu-item index="2-1-1"><i class="el-icon-lock" />资源列表</el-menu-item>
              <el-menu-item index="2-1-2"><i class="el-icon-lock" />添加节点</el-menu-item>
            </el-sub-menu>
            <el-menu-item-group>
              <el-menu-item index="2-2"><i class="el-icon-lock" />资源发现</el-menu-item>
            </el-menu-item-group>
            <el-menu-item-group>
              <el-menu-item index="2-3"><i class="el-icon-lock" />维护计划</el-menu-item>
            </el-menu-item-group>
            <el-menu-item-group>
              <el-menu-item index="2-4"><i class="el-icon-lock" />属性标签</el-menu-item>
            </el-menu-item-group>
            <el-menu-item-group>
              <el-menu-item index="2-5"><i class="el-icon-lock" />模板管理</el-menu-item>
            </el-menu-item-group>
         </el-sub-menu>
          <el-sub-menu index="3">
            <template #title>
              <span>模块管理</span>
            </template>
            <el-menu-item-group>
              <el-menu-item index="3-1"><i class="el-icon-lock" />模块管理</el-menu-item>
            </el-menu-item-group>
          </el-sub-menu>
          <el-sub-menu index="4">
            <template #title>
              <span>告警管理</span>
            </template>
            <el-menu-item-group>
              <el-menu-item index="4-1"><i class="el-icon-lock" />活跃告警</el-menu-item>
            </el-menu-item-group>
            <el-menu-item-group>
              <el-menu-item index="4-2"><i class="el-icon-lock" />告警设置</el-menu-item>
            </el-menu-item-group>
            <el-menu-item-group>
              <el-menu-item index="4-3"><i class="el-icon-lock" />告警动作</el-menu-item>
            </el-menu-item-group>
          </el-sub-menu>
          <el-sub-menu index="5">
            <template #title>
              <span>报表管理</span>
            </template>
            <el-sub-menu index="5-1">
              <template #title>报表管理</template>
              <el-menu-item index="5-1-1"><i class="el-icon-lock" />报表汇总</el-menu-item>
              <el-menu-item index="5-1-2"><i class="el-icon-lock" />报表设置</el-menu-item>
            </el-sub-menu>
            <el-sub-menu index="5-2">
              <template #title>策略管理</template>
              <el-menu-item index="5-2-1"><i class="el-icon-lock" />策略汇总</el-menu-item>
              <el-menu-item index="5-2-2"><i class="el-icon-lock" />策略设置</el-menu-item>
            </el-sub-menu>
          </el-sub-menu>
          <el-sub-menu index="6">
            <template #title>
              <span>拓扑管理</span>
            </template>
            <el-menu-item-group>
              <el-menu-item index="6-1"><i class="el-icon-lock" />网络拓扑图</el-menu-item>
            </el-menu-item-group>
            <el-menu-item-group>
              <el-menu-item index="6-2"><i class="el-icon-lock" />自定义图标</el-menu-item>
            </el-menu-item-group>
          </el-sub-menu>
          <el-sub-menu index="7">
            <template #title>
              <span>网络配置管理</span>
            </template>
            <el-menu-item-group>
              <el-menu-item index="7-1"><i class="el-icon-lock" />网络配置管理</el-menu-item>
            </el-menu-item-group>
          </el-sub-menu>
          <el-sub-menu index="8">
            <template #title>
              <span>日志管理</span>
            </template>
            <el-menu-item-group>
              <el-menu-item index="8-1"><i class="el-icon-lock" />日志汇总</el-menu-item>
            </el-menu-item-group>
            <el-menu-item-group>
              <el-menu-item index="8-2"><i class="el-icon-lock" />日志分析</el-menu-item>
            </el-menu-item-group>
          </el-sub-menu>
          <el-sub-menu index="9">
            <template #title>
              <span>用户管理</span>
            </template>
            <el-sub-menu index="9-1">
              <template #title>账号管理</template>
              <el-menu-item index="9-1-1"><i class="el-icon-lock" />账号信息</el-menu-item>
              <el-menu-item index="9-1-2"><i class="el-icon-lock" />创建账号</el-menu-item>
            </el-sub-menu>
            <el-sub-menu index="9-2">
              <template #title>角色管理</template>
              <el-menu-item index="9-2-1"><i class="el-icon-lock" />角色信息</el-menu-item>
              <el-menu-item index="9-2-2"><i class="el-icon-lock" />创建角色</el-menu-item>
            </el-sub-menu>
            <el-sub-menu index="9-3">
              <template #title>分组管理</template>
              <el-menu-item index="9-3-1"><i class="el-icon-lock" />分组信息</el-menu-item>
              <el-menu-item index="9-3-2"><i class="el-icon-lock" />创建分组</el-menu-item>
            </el-sub-menu>
          </el-sub-menu>
          <el-sub-menu index="10">
            <template #title>
              <span>系统管理</span>
            </template>
            <el-menu-item-group>
              <el-menu-item index="10-1"><i class="el-icon-lock" />我的部署环境</el-menu-item>
            </el-menu-item-group>
            <el-menu-item-group>
              <el-menu-item index="10-2"><i class="el-icon-lock" />许可证管理</el-menu-item>
            </el-menu-item-group>
            <el-menu-item-group>
              <el-menu-item index="10-3"><i class="el-icon-lock" />轮询引擎管理</el-menu-item>
            </el-menu-item-group>
            <el-menu-item-group>
              <el-menu-item index="10-4"><i class="el-icon-lock" />凭证管理</el-menu-item>
            </el-menu-item-group>
            <el-menu-item-group>
              <el-menu-item index="10-5"><i class="el-icon-lock" />事件管理</el-menu-item>
            </el-menu-item-group>
            <el-menu-item-group>
              <el-menu-item index="10-6"><i class="el-icon-lock" />密码管理</el-menu-item>
            </el-menu-item-group>
          </el-sub-menu>
          <!-- demo测试-->
          <el-sub-menu index="11">
            <template #title>
              <span>资源管理</span>
            </template>
            <el-menu-item-group>
              <el-menu-item index="/swiper"><i class="el-icon-picture el-icon-lock" />轮播图配置</el-menu-item>
              <el-menu-item index="/hot"><i class="el-icon-star-on el-icon-lock" />热销商品配置</el-menu-item>
              <el-menu-item index="/new"><i class="el-icon-sell el-icon-lock" />新品上线配置</el-menu-item>
              <el-menu-item index="/recommend"><i class="el-icon-thumb el-icon-lock" />为你推荐配置</el-menu-item>
            </el-menu-item-group>
          </el-sub-menu>
          <el-sub-menu index="12">
            <template #title>
              <span>模块管理</span>
            </template>
            <el-menu-item-group>
              <el-menu-item index="/category"><i class="el-icon-menu el-icon-lock" />分类管理</el-menu-item>
              <el-menu-item index="/good"><i class="el-icon-s-goods el-icon-lock" />商品管理</el-menu-item>
              <el-menu-item index="/guest"><i class="el-icon-user-solid el-icon-lock" />会员管理</el-menu-item>
              <el-menu-item index="/order"><i class="el-icon-s-order el-icon-lock" />订单管理</el-menu-item>
            </el-menu-item-group>
          </el-sub-menu>

        </el-menu>
      </el-aside>
      <el-container class="content">
        <Header />
        <div class="main">
          <router-view />
        </div>
        <Footer />
      </el-container>
    </el-container>
    <el-container v-else class="container">
      <router-view />
    </el-container>
  </div>
</template>

<script>
import { reactive, toRefs } from 'vue'
import { useRouter } from 'vue-router'
import Header from '@/components/Header.vue'
import Footer from '@/components/Footer.vue'
import { localGet, pathMap } from '@/utils'
export default {
  name: 'App',
  components: {
    Header,
    Footer
  },
  setup() {
    const noMenu = ['/login']
    const router = useRouter()
    const state = reactive({
      showMenu: true,
      defaultOpen: ['1'],
      currentPath: '/',
    })

    router.beforeEach((to, from, next) => {
      if (to.path == '/login') {
        // 如果路径是 /login 则正常执行
        next()
      } else {
        // 如果不是 /login，判断是否有 token
        if (!localGet('token')) {
          // 如果没有，则跳至登录页面
          next({ path: '/login' })
        } else {
          // 否则继续执行
          next()
        }
      }
      state.showMenu = !noMenu.includes(to.path)
      state.currentPath = to.path
      document.title = pathMap[to.name]
    })

    return {
      ...toRefs(state)
    }
  }
}
</script>

<style scoped>
.layout {
  min-height: 100vh;
  background-color: #ffffff;
}
.container {
  height: 100vh;
}
.aside {
  width: 200px!important;
  background-color: #222832;
}
.head {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 50px;
}
.head > div {
  display: flex;
  align-items: center;
}

.head img {
  width: 50px;
  height: 50px;
  margin-right: 10px;
}
.head span {
  font-size: 20px;
  color: #ffffff;
}
.line {
  border-top: 1px solid hsla(0,0%,100%,.05);
  border-bottom: 1px solid rgba(0,0,0,.2);
}
.content {
  display: flex;
  flex-direction: column;
  max-height: 100vh;
  overflow: hidden;
}
.main {
  height: calc(100vh - 100px);
  overflow: auto;
  padding: 10px;
}

</style>

<style>
body {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
.el-menu {
  border-right: none!important;
}
.el-submenu {
  border-top: 1px solid hsla(0, 0%, 100%, .05);
  border-bottom: 1px solid rgba(0, 0, 0, .2);
}
.el-submenu:first-child {
  border-top: none;
}
.el-submenu [class^="el-icon-"] {
  vertical-align: -1px!important;
}
a {
  color: #409eff;
  text-decoration: none;
}
.el-pagination {
  text-align: center;
  margin-top: 20px;
}
.el-popper__arrow {
  display: none;
}
</style>
