# 简化版创建步骤

::: tip
此文仅内部开发使用，虽对外展示，但是没有实用意义，请读者忽略。
:::

本文介绍如何将完整版 D2 Admin 化简为简化版

## 仓库准备

[仓库地址](https://github.com/d2-projects/d2-admin-start-kit)

在本地建立一个新功能：

![](http://fairyever.qiniudn.com/20180904140651.png?imageMogr2/auto-orient/thumbnail/1480x/blur/1x0/quality/100|imageslim)

名称和现在完整版最新的版本号对应：

![](http://fairyever.qiniudn.com/20180904140839.png?imageMogr2/auto-orient/thumbnail/1480x/blur/1x0/quality/100|imageslim)

![](http://fairyever.qiniudn.com/20180904140918.png?imageMogr2/auto-orient/thumbnail/1480x/blur/1x0/quality/100|imageslim)

新的分支：

![](http://fairyever.qiniudn.com/20180904140950.png?imageMogr2/auto-orient/thumbnail/1480x/blur/1x0/quality/100|imageslim)

## 备份和替换文件

删除依赖：

![](http://fairyever.qiniudn.com/20180904141557.png?imageMogr2/auto-orient/thumbnail/1480x/blur/1x0/quality/100|imageslim)

备份文件：

![](http://fairyever.qiniudn.com/20180904141636.png?imageMogr2/auto-orient/thumbnail/1480x/blur/1x0/quality/100|imageslim)

删除原始项目文件：

![](http://fairyever.qiniudn.com/20180904141727.png?imageMogr2/auto-orient/thumbnail/1480x/blur/1x0/quality/100|imageslim)

复制完整版的项目文件至简化版项目：

![](http://fairyever.qiniudn.com/20180904141835.png?imageMogr2/auto-orient/thumbnail/1480x/blur/1x0/quality/100|imageslim)

## 删除文件夹

* 删除 .github 文件夹（隐藏文件）
* 删除 doc
* 删除 src/pages/demo
* 删除 public/markdown
* 删除 public/image/baidu-pan-logo.png
* 删除 src/api/components
* 删除 src/api/demo
* 删除 src/mock/api/demo

## 删除无用的 svg 图标

只保留两个系统图标：

![](http://fairyever.qiniudn.com/20180904143712.png?imageMogr2/auto-orient/thumbnail/1480x/blur/1x0/quality/100|imageslim)

## 删除无用的样式补丁

* 删除 src/assets/style/fixed/markdown.scss
* 删除 src/assets/style/fixed/tree-view.scss
* 删除 src/assets/style/fixed/vue-grid-layout.scss
* 删除 src/assets/style/fixed/vue-splitpane.scss

更新 src/assets/style/public-class.scss 导入部分

``` scss
@import 'public';

// 补丁 base
@import '~@/assets/style/fixed/base.scss';
// 补丁 element
@import '~@/assets/style/fixed/element.scss';

// 动画
@import '~@/assets/style/animate/vue-transition.scss';
```

## 删除不必要组件

* 删除 src/components/d2-container-frame
* 删除 src/components/d2-count-up
* 删除 src/components/d2-highlight
* 删除 src/components/d2-icon-select
* 删除 src/components/d2-link-btn
* 删除 src/components/d2-markdown
* 删除 src/components/d2-mde
* 删除 src/components/d2-quill

将 src/components/index.js 重写为

``` js
import Vue from 'vue'

import d2Container from './d2-container'

// 注意 有些组件使用异步加载会有影响
Vue.component('d2-container', d2Container)
Vue.component('d2-page-cover', () => import('./d2-page-cover'))
Vue.component('d2-icon', () => import('./d2-icon'))
Vue.component('d2-icon-svg', () => import('./d2-icon-svg/index.vue'))
```

## menu 设置

删除 src/menu 下面的所有文件

写入新的文件：

aside.js：

``` js
// 菜单 侧边栏
export default [
  { path: '/index', title: '首页', icon: 'home' },
  {
    title: '页面',
    icon: 'folder-o',
    children: [
      { path: '/page1', title: '页面 1' },
      { path: '/page2', title: '页面 2' },
      { path: '/page3', title: '页面 3' }
    ]
  }
]
```

header.js

``` js
// 菜单 顶栏
export default [
  { path: '/index', title: '首页', icon: 'home' },
  {
    title: '页面',
    icon: 'folder-o',
    children: [
      { path: '/page1', title: '页面 1' },
      { path: '/page2', title: '页面 2' },
      { path: '/page3', title: '页面 3' }
    ]
  }
]
```

## 示例页面

从简化版的备份中将三个示例页面放到新的项目中：

![](http://fairyever.qiniudn.com/20180904144230.png?imageMogr2/auto-orient/thumbnail/1480x/blur/1x0/quality/100|imageslim)

## 删除插件

* 删除 src/plugin/export
* 删除 src/plugin/import

删除 src/plugin/d2admin/index.js 中涉及已经删除插件的导入部分

## router

重写 src/router/routes.js

``` js
// layout
import layoutHeaderAside from '@/layout/header-aside'

const meta = { requiresAuth: true }

/**
 * 在主框架内显示
 */
const frameIn = [
  {
    path: '/',
    redirect: { name: 'index' },
    component: layoutHeaderAside,
    children: [
      {
        path: 'index',
        name: 'index',
        meta,
        component: () => import('@/pages/index')
      },
      {
        path: '/page1',
        name: 'page1',
        component: () => import('@/pages/page1'),
        meta: { meta, title: '页面 1' }
      },
      {
        path: '/page2',
        name: 'page2',
        component: () => import('@/pages/page2'),
        meta: { meta, title: '页面 2' }
      },
      {
        path: '/page3',
        name: 'page3',
        component: () => import('@/pages/page3'),
        meta: { meta, title: '页面 3' }
      }
    ]
  }
]

/**
 * 在主框架之外显示
 */
const frameOut = [
  // 登陆
  {
    path: '/login',
    name: 'login',
    component: () => import('@/pages/login')
  }
]

/**
 * 错误页面
 */
const errorPage = [
  // 404
  {
    path: '*',
    name: '404',
    component: () => import('@/pages/error-page-404')
  }
]

// 导出需要显示菜单的
export const frameInRoutes = frameIn

// 重新组织后导出
export default [
  ...frameIn,
  ...frameOut,
  ...errorPage
]
```

## main.js

* 删除不必须的插件

* 重写菜单和路由设置

``` js
// 菜单和路由设置
import router from './router'
import menuHeader from '@/menu/header'
import menuAside from '@/menu/aside'
import { frameInRoutes } from '@/router/routes'
```

* 在 created 生命周期钩子中增加设置侧边栏菜单的代码

``` js
// 设置侧边栏菜单
this.$store.commit('d2admin/menu/asideSet', menuAside)
```

* 删除设置侧边栏菜单的逻辑

``` js
watch: {
  // 监听路由 控制侧边栏显示
  '$route.matched' (val) {
    const _side = menuAside.filter(menu => menu.path === val[0].path)
    this.$store.commit('d2admin/menu/asideSet', _side.length > 0 ? _side[0].children : [])
  }
}
```

## 删除依赖

* @d2-projects/d2-crud
* clipboard-polyfill
* countup.js
* echarts
* file-saver
* github-markdown-css
* highlight.js
* marked
* papaparse
* quill
* simplemde
* v-charts
* v-contextmenu
* vue-grid-layout
* vue-json-tree-view
* vue-splitpane
* xlsx

``` shell
npm remove @d2-projects/d2-crud clipboard-polyfill countup.js echarts file-saver github-markdown-css highlight.js marked papaparse quill simplemde v-charts v-contextmenu vue-grid-layout vue-json-tree-view vue-splitpane xlsx --save
```

## vue.config.js

``` js
const baseUrl = '/d2-admin-start-kit/'
```

## 测试

``` shell
npm i
npm run dev
```

::: tip
简化版代码 `de358376fd85791edd2acd3049956aa3`
:::

## 提交代码

![](http://fairyever.qiniudn.com/20180904152221.png?imageMogr2/auto-orient/thumbnail/1480x/blur/1x0/quality/100|imageslim)

如果是小改动的话可以只覆盖某些文件，无需像本文中介绍这样全部重新覆盖。