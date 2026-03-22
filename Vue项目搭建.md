# Vue项目搭建

安装Node.js后要安装Vue CLI

```bash
# 检查是否已安装以及其版本
npm -v
node -v

# 全局安装 @vue/cli
npm install -g @vue/cli
# 切换到淘宝镜像源以加速安装
npm config set registry https://registry.npmmirror.com
```

创建项目

```bash
vue create my-vue-app
```

> 请将 `my-vue-app` 替换为您想要的项目名称。

执行该命令后，系统会提示您选择一个预设（preset）。对于初学者，建议选择 **Default ([Vue 3] babel, eslint)** 或 **Default (Vue 2) babel, eslint**，这会自动配置好常用的工具。

```
? Please pick a preset:
  Default ([Vue 3] babel, eslint)
  Default (Vue 2) babel, eslint
  Manually select features # 手动选择功能
> Default ([Vue 3] babel, eslint)
```

选择Manually select features有下面这些选择

```
? Check the features needed for your project:
>( ) Choose Vue version          # 选择 Vue 的版本 (2.x or 3.x)
 ( ) Babel                       # ES6+ 语法转译，让你能使用最新的 JavaScript 特性
 ( ) TypeScript                  # 支持 TypeScript
 ( ) Progressive Web App (PWA)   # 支持渐进式Web应用
 ( ) Router                      # Vue Router，支持单页应用(SPA)的页面导航和路由
 ( ) Vuex                        # Vuex，Vue 的状态管理模式，用于集中管理组件的状态
 ( ) CSS Pre-processors          # CSS 预处理器，如 Sass, Less, Stylus
 ( ) Linter / Formatter          # 代码风格检查和格式化工具，如 ESLint, Prettier
 ( ) Unit Testing                # 单元测试框架，如 Jest, Mocha + Chai
 ( ) E2E Testing                 # 端到端(E2E)测试框架，如 Cypress, Nightwatch
```

因为vue版本^2.6.14下载对应的组件库

```bash
npm install vue-router@3.6.5 vuex@3.6.2 axios@0.27.2
npm i element-ui -S
npm install sass -D
npm install sass-loader -D
```

