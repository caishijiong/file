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



# yarn包管理改成pnpm包管理

### 1、全局安装pnpm

```bash
npm install -g pnpm
pnpm -v # 查看版本，检测是否安装成功
```

### 2、清除现有依赖文件

在项目根目录下删除原有的依赖文件：

```bash
# Windows PowerShell
Remove-Item -Recurse -Force node_modules
Remove-Item -Force yarn.lock
Remove-Item -Force package-lock.json

# macOS / Linux
# rm -rf node_modules yarn.lock package-lock.json
```

如果某个锁文件不存在，提示找不到文件可忽略。

### 3、转换锁定文件

使用 pnpm 提供的导入功能，从 yarn.lock 生成 pnpm-lock.yaml：

```bash
pnpm import
```

此命令会根据现有的 yarn.lock 文件生成对应的 pnpm-lock.yaml 文件。若项目没有 yarn.lock，可跳过此步骤。

### 4、安装依赖

```bash
pnpm install
```

### 5、运行项目

运行项目，检查是否有依赖相关的错误：

```bash
# Vue CLI 项目（通常是 vue create 创建的）
pnpm run serve

# Vite 项目
# pnpm run dev
```

### 6、更新脚本命令

一般不需要把 package.json 的 scripts 从 yarn 改为 pnpm。
只需要把日常执行命令改为 pnpm，例如：

```bash
yarn add axios        -> pnpm add axios
yarn add -D sass      -> pnpm add -D sass
yarn remove axios     -> pnpm remove axios
yarn run serve        -> pnpm run serve
```



## **注意事项**

1. **幽灵依赖**：pnpm 使用严格的依赖管理，不会创建扁平化的 node_modules 结构，因此可能存在之前能访问但现在无法访问的"幽灵依赖"，需要手动添加。
2. **Peer Dependencies**：pnpm 对 peer dependencies 的处理更严格，可能需要手动解决冲突。
3. **老项目兼容**：如果是 Vue2 + element-ui 等老项目，出现模块解析异常时，可在 .npmrc 中尝试增加 `shamefully-hoist=true`。
4. **CI/CD 配置**：更新持续集成配置，确保使用 pnpm 命令安装依赖。
5. **团队同步**：通知团队成员迁移至 pnpm，并更新开发环境。
