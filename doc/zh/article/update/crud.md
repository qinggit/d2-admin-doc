# D2 CRUD

D2 Crud，一款简单易用的表格组件

[D2-Crud](https://github.com/d2-projects/d2-crud) 是一套基于[Vue.js 2.2.0+](https://cn.vuejs.org/) 和 [Element UI 2.0.0+](http://element-cn.eleme.io/#/zh-CN) 的表格组件。`D2-Crud` 将 `Element` 的功能进行了封装，并增加了表格的增删改查、数据校验、表格内编辑等常用的功能。大部分功能可由配置 `json` 实现，在实现并扩展了 `Elememt` 表格组件功能的同时，降低了开发难度，减少了代码量，大大简化了开发流程。

GitHub：<https://github.com/d2-projects/d2-crud>

文档：<https://d2-projects.github.io/d2-admin-doc/zh/ecosystem-d2-crud/>

示例：<https://d2-projects.github.io/d2-admin/#/demo/d2-crud/index>

> 示例部署在 Github Pages 如果您的网络不太好（示例项目中包含大量示例，体积较大），请完整克隆 [项目](https://github.com/d2-projects/d2-admin) 在本地启动。

## 作者

发表此文的账号并不是 [D2-Crud](https://github.com/d2-projects/d2-crud) 原作者账号。

作者掘金地址：[@被遗忘的传说](https://juejin.im/user/588341d7128fe1006c317b3d)。

作者 github [sunhaoxiang](https://github.com/sunhaoxiang)

欢迎大家关注支持他，也支持我们继续开源 ~

## 功能简介

- 继承了 Element 中表格所有功能
- 表格新增数据
- 表格修改数据
- 表格删除数据
- 使用 Element 中的组件渲染表格内容和表单编辑内容
- 表单编辑校验
- 表格内直接编辑模式

## 如何使用
使用npm安装：
``` bash
npm i element-ui @d2-projects/d2-crud -S
```

使用yarn安装：
``` bash
yarn add element-ui @d2-projects/d2-crud
```

在 `main.js` 中写入以下内容：
``` js
import Vue from 'vue'
import ElementUI from 'element-ui'
import 'element-ui/lib/theme-chalk/index.css'
import D2Crud from '@d2-projects/d2-crud'

Vue.use(ElementUI)
Vue.use(D2Crud)

new Vue({
  el: '#app',
  render: h => h(App)
})
```

一个简单的表格示例：
``` html
<template>
  <div>
    <d2-crud
      ref="d2Crud"
      :columns="columns"
      :data="data"/>
  </div>
</template>

<script>
export default {
  data () {
    return {
      columns: [
        {
          title: '日期',
          key: 'date'
        },
        {
          title: '姓名',
          key: 'name'
        },
        {
          title: '地址',
          key: 'address'
        }
      ],
      data: [
        {
          date: '2016-05-02',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄'
        },
        {
          date: '2016-05-04',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1517 弄'
        },
        {
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1519 弄'
        },
        {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1516 弄'
        }
      ]
    }
  }
}
</script>
```

下图是上述代码片段的渲染结果：

## 示例

### 新增数据
![新增数据](https://user-gold-cdn.xitu.io/2018/9/3/1659d305eb1d45f3?w=1424&h=750&f=gif&s=835367)
演示地址：<https://d2-projects.github.io/d2-admin/#/demo/d2-crud/demo16>

### 修改数据
![修改数据](https://user-gold-cdn.xitu.io/2018/9/3/1659d305e0cb4af7?w=1424&h=750&f=gif&s=581016)
演示地址：<https://d2-projects.github.io/d2-admin/#/demo/d2-crud/demo17>

### 删除数据
![删除数据](https://user-gold-cdn.xitu.io/2018/9/3/1659d305de0680b3?w=1424&h=750&f=gif&s=716098)
演示地址：<https://d2-projects.github.io/d2-admin/#/demo/d2-crud/demo18>

### 表单校验
![表单校验](https://user-gold-cdn.xitu.io/2018/9/3/1659d305e444175d?w=1424&h=750&f=gif&s=402618)
演示地址：<https://d2-projects.github.io/d2-admin/#/demo/d2-crud/demo22>

### 表格内编辑
![表格内编辑](https://user-gold-cdn.xitu.io/2018/9/3/1659d305e23181ac?w=1424&h=750&f=gif&s=382246)
演示地址：<https://d2-projects.github.io/d2-admin/#/demo/d2-crud/demo23>

## 代码对比

一个带有编辑删除功能的例子与直接使用 `Element UI` 的代码对比

使用D2 Crud：

``` html
<template>
  <div>
    <d2-crud
      ref="d2Crud"
      :columns="columns"
      :data="data"
      index-row
      selection-row
      :rowHandle="rowHandle"
      :form-template="formTemplate"
      @row-edit="handleRowEdit"
      @row-remove="handleRowRemove"/>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        columns: [
          {
            title: '日期',
            key: 'date'
          },
          {
            title: '姓名',
            key: 'name'
          },
          {
            title: '地址',
            key: 'address'
          }
        ],
        data: [
          {
            date: '2016-05-02',
            name: '王小虎',
            address: '上海市普陀区金沙江路 1518 弄'
          },
          {
            date: '2016-05-04',
            name: '王小虎',
            address: '上海市普陀区金沙江路 1517 弄'
          },
          {
            date: '2016-05-01',
            name: '王小虎',
            address: '上海市普陀区金沙江路 1519 弄'
          },
          {
            date: '2016-05-03',
            name: '王小虎',
            address: '上海市普陀区金沙江路 1516 弄'
          }
        ],
        rowHandle: {
          edit: {
            size: 'mini'
          },
          remove: {
            size: 'mini'
          }
        },
        formTemplate: {
          date: {
            title: '日期',
            value: ''
          },
          name: {
            title: '姓名',
            value: ''
          },
          address: {
            title: '地址',
            value: ''
          }
        }
      }
    },
    methods: {
      handleRowEdit ({index, row}, done) {
        this.$message({
          message: '编辑成功',
          type: 'success'
        })
        done()
      },
      handleRowRemove ({index, row}, done) {
        this.$message({
          message: '删除成功',
          type: 'success'
        })
        done()
      }
    }
  }
</script>
```

直接使用Element UI的表格组件：

``` html
<template>
  <div>
    <el-table
      :data="tableData">
      <el-table-column
        type="selection"
        width="55">
      </el-table-column>
      <el-table-column
        type="index"
        width="50">
      </el-table-column>
      <el-table-column
        prop="date"
        label="日期">
      </el-table-column>
      <el-table-column
        prop="name"
        label="姓名">
      </el-table-column>
      <el-table-column
        prop="address"
        label="地址">
      </el-table-column>
      <el-table-column label="操作">
        <template slot-scope="scope">
          <el-button
            size="mini"
            @click="handleEdit(scope.$index, scope.row)">编辑</el-button>
          <el-button
            size="mini"
            type="danger"
            @click="handleDelete(scope.$index, tableData)">删除</el-button>
        </template>
      </el-table-column>
    </el-table>
    <el-dialog
      title="编辑"
      :visible.sync="showDialog">
      <el-form>
        <el-form-item label="日期">
          <el-input v-model="form.date"></el-input>
        </el-form-item>
        <el-form-item label="姓名">
          <el-input v-model="form.name"></el-input>
        </el-form-item>
        <el-form-item label="地址">
          <el-input v-model="form.address"></el-input>
        </el-form-item>
      </el-form>
      <span slot="footer" class="dialog-footer">
        <el-button type="primary" @click="handleEditSave">确 定</el-button>
      </span>
    </el-dialog>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        tableData: [
          {
            date: '2016-05-02',
            name: '王小虎',
            address: '上海市普陀区金沙江路 1518 弄'
          },
          {
            date: '2016-05-04',
            name: '王小虎',
            address: '上海市普陀区金沙江路 1517 弄'
          },
          {
            date: '2016-05-01',
            name: '王小虎',
            address: '上海市普陀区金沙江路 1519 弄'
          },
          {
            date: '2016-05-03',
            name: '王小虎',
            address: '上海市普陀区金沙江路 1516 弄'
          }
        ],
        form: {
          date: '',
          name: '',
          address: ''
        },
        showDialog: false
      }
    },
    methods: {
      handleEdit (index, row) {
        this.showDialog = true
        this.editIndex = index
        this.form = row
        this.$message({
          message: '编辑成功',
          type: 'success'
        })
      },
      handleEditSave () {
        this.showDialog = false
      },
      handleDelete (index, rows) {
        this.$confirm('是否删除?', '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning'
        }).then(() => {
          rows.splice(index, 1)
          this.$message({
            message: '删除成功',
            type: 'success'
          })
        })
      }
    }
  }
</script>
```

## D2 Projects

团队主页：<https://github.com/d2-projects>

如果你看完了，并且觉得还不错，希望可以到团队主上给我们的项目点一个 **star** 作为你对我们的认可与支持，谢谢。

## 加入小组

开源项目组官方公众号，关注及时获得最新更新资讯、文档地址、相关的技术文章：

<img src="https://user-gold-cdn.xitu.io/2018/8/23/1656484863509697?w=344&h=344&f=png&s=46090" style="width: 200px;"/>

2000 人 QQ 交流群，及时答疑解惑：

<img src="https://user-gold-cdn.xitu.io/2018/9/3/1659d4d65f861537?w=540&h=740&f=jpeg&s=97734" style="width: 200px;"/>

如果需要加微信群，请关注公众号在底部菜单获取二维码。