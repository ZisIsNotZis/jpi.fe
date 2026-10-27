<p align="center">
  <img src="assets/logo.svg" width="96" height="96" alt="jpi.fe logo">
</p>

<h1 align="center">jpi.fe</h1>

<p align="center"><strong>像阅读 JSON 一样编辑它：一棵由表格组成的树。</strong></p>

<p align="center">
  <a href="README.md">English</a> · <strong>简体中文</strong>
</p>

jpi.fe 是一个 Vue 3 单页应用，能把任意 JSON 文档渲染成层层嵌套的可编辑表格。对象和数组变成表格，标量变成行内输入框，同一对组件在任意深度递归复用。你可以新增行、列或键，修改值，再把该节点保存回 API。

这是 2024 年的原型，现作为存档保留。它当年对接的 REST 后端不在本仓库中。

## 快速开始

```sh
npm install
npm run dev
```

打开 Vite 输出的地址（通常是 `http://localhost:5173`）。实体列表和翻页使用写死在
[`src/App.vue`](src/App.vue) 中的协议相对基地址 `//127.0.0.1:8080/api`；没有匹配的后端时，内置示例文档仍会显示，但加载和保存不可用。

## 现在能做什么

- 递归渲染任意形状 JSON 中的数组、对象和标量
- 行内编辑标量，增删对象的键
- 增删表格行，为整张表增删列
- 通过 REST 接口保存或删除单个节点
- 在实体之间切换并翻页
- 无数据时显示一份内置示例文档

## 架构

```text
src/
  main.js                 挂载应用
  App.vue                 实体选择、分页、axios 请求
  components/
    Trees.vue             递归分发：数组 / 对象 / null / 标量
    Tables.vue            数组与对象的表格视图，行内编辑
```

`Trees.vue` 是核心：它判断值的类型，并为子节点递归渲染自己，因此嵌套深度只受文档本身限制。`App.vue` 负责全部 HTTP 请求，并把当前文档保存在 `dat` 中。项目没有路由、状态库或测试。

存档说明见 [`docs/project-status.md`](docs/project-status.md)。

## 如何开发

- 需要 Node.js 18+ 与 npm；依赖为 Vue 3.4、Axios 和 Vite 5。
- `npm run dev` 启动带热更新的 Vite 开发服务器。
- `npm run build` 输出生产包到 `dist/`；`npm run preview` 本地预览。
- [`vite.config.js`](vite.config.js) 把 `@/` 别名指向 `src/`。
- 若要连接其他服务，改动 [`src/App.vue`](src/App.vue) 中的 API 基地址（所有请求共用）。

## 如何贡献

本仓库已归档，不再积极维护，因此没有路线图承诺。欢迎提交能修复明确缺陷的 issue 和小型 pull request——如何运行、唯一存在的检查（`npm run build`）以及 pull request 应包含什么，见 [`CONTRIBUTING.md`](CONTRIBUTING.md)。

## 路线图

**已实现**

- 任意 JSON 的递归渲染
- 行内编辑，以及行、列、键和数组项的增删
- 对分页 REST API 的保存与删除请求
- 实体切换与翻页

**计划中 / 尚未实现**

- 可配置的 API 基地址，替代写死的 `127.0.0.1:8080`
- 一个小型 mock 后端或演示模式，让界面可以独立运行
- 测试、撤销和键盘导航
- 清理残留的 Vite 模板包名（`vue-project`）

**未来设想**

最初的想法是做一个面向任意 JSON 的通用管理界面：一对递归组件就能把任何文档变成可编辑、类似电子表格的树，这样小型内部工具不必各自实现一套编辑器。这个方向仍然值得做；本仓库只是它最早、尚未完成的草稿。

## 许可证

GNU Affero 通用公共许可证 v3.0 only —— 见 [`LICENSE`](LICENSE)。第三方依赖保留各自的许可证。
