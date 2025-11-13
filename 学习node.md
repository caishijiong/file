# 学习node

## Nood.js

### 一些命令

```javascript
`命令npm init` 初始化一个新的 npm 项目，创建 package.json 文件。

Package.json
name：项目名称，必须是唯一的字符串，通常采用小写字母和连字符的组合。

version：项目版本号，通常采用语义化版本号规范。

description：项目描述。

main：项目的主入口文件路径，通常是一个 JavaScript 文件。

keywords：项目的关键字列表，方便他人搜索和发现该项目。

author：项目作者的信息，包括姓名、邮箱、网址等。

license：项目的许可证类型，可以是自定义的许可证类型或者常见的开源许可证（如 MIT、Apache 等）。

`package.json文件中的三种依赖类型:`dependencies`(生产环境依赖)`、devDependenices`(开发依赖)`和peerDependencies`(对等依赖)`
dependencies：项目所依赖的包的列表，这些包会在项目运行时自动安装。
devDependencies：项目开发过程中所需要的包的列表，这些包不会随项目一起发布，而是只在开发时使用。
peerDependencies：项目的同级依赖，即项目所需要的模块被其他模块所依赖。

scripts：定义了一些脚本命令，比如启动项目、运行测试等。

repository：项目代码仓库的信息，包括类型、网址等。

bugs：项目的 bug 报告地址。

homepage：项目的官方网站地址或者文档地址。

`命令npm config list`: 用于列出所有的 npm 配置信息。执行该命令可以查看当前系统和用户级别的所有 npm 配置信息，以及当前项目的配置信息（如果在项目目录下执行该命令）

`命令npm get registry`: 查看地址
`npm官网： https://registry.npmjs.org/`
`淘宝镜像： http://registry.npm.taobao.org/`

`全局安装可执行文件的命令`： npm ls -g

`react脚手架`：npm install -g create-react-app
```

## npm install

```mermaid
graph TD
    A[npm install] --> B[package.json]
    A --> C[package-lock.json]
    A --> D[配置文件]
    
    D --> E[用户 .npmrc]
    D --> F[全局 .npmrc]
    D --> G[项目 .npmrc]
    
    B --> H[版本定义]
    B --> I[依赖项]
    
    C --> J[锁定版本]
    C --> K[完整性校验]
    
    H --> L[版本控制]
    I --> L
    J --> L
    K --> L
    
    L --> M[权限控制]
    M --> N[下载权限]
    M --> O[性能完整性]
    M --> P[添加权限]
    
    N --> Q[有/无]
    O --> R[校验通过/失败]
    P --> S[更新package-lock.json]
    
    style A fill:#f9f,stroke:#333
    style B fill:#bbf,stroke:#333
    style C fill:#bbf,stroke:#333
```



```sh
.npmrc文件可以配置的文件

registry=http://registry.npmjs.org/
# 定义npm的registry，即npm的包下载源

proxy=http://proxy.example.com:8080/
# 定义npm的代理服务器，用于访问网络

https-proxy=http://proxy.example.com:8080/
# 定义npm的https代理服务器，用于访问网络

strict-ssl=true
# 是否在SSL证书验证错误时退出

cafile=/path/to/cafile.pem
# 定义自定义CA证书文件的路径

user-agent=npm/{npm-version} node/{node-version} {platform}
# 自定义请求头中的User-Agent

save=true
# 安装包时是否自动保存到package.json的dependencies中

save-dev=true
# 安装包时是否自动保存到package.json的devDependencies中

save-exact=true
# 安装包时是否精确保存版本号

engine-strict=true
# 是否在安装时检查依赖的node和npm版本是否符合要求

scripts-prepend-node-path=true
# 是否在运行脚本时自动将node的路径添加到PATH环境变量中
```

## npm run

```ABAP
用npm run vite举例

先从当前项目的 node_modules/.bin 去查找可执行命令vite
如果没找到就去全局的 node_modules 去找可执行命令vite
如果还没找到就去环境变量查找
再找不到就进行报错

"predev": "node prev.js",
"dev": "node index.js",
"postdev": "node post.js"

执行 npm run dev 命令的时候 predev 会自动执行 
他的生命周期是在dev之前执行，然后执行dev命令，再然后执行postdev，也就是dev之后执行
```

## npx

避免全局安装：`npx`允许你执行npm package，而不需要你先全局安装它。

总是使用最新版本：如果你没有在本地安装相应的npm package，`npx`会从npm的package仓库中下载并使用最新版。

执行任意npm包：`npx`不仅可以执行在`package.json`的`scripts`部分定义的命令，还可以执行任何npm package。

执行GitHub gist：`npx`甚至可以执行GitHub gist或者其他公开的JavaScript文件。



`npx` 侧重于执行命令的，执行某个模块命令。虽然会自动安装模块，但是重在执行某个命令

`npm` 侧重于安装或者卸载某个模块的。重在安装，并不具备执行某个模块的功能。

## 发布npm包

```ABAP
发布npm的包的好处是什么

方便团队或者跨团队共享代码，使用npm包就可以方便的管理，并且还可以进行版本控制
做开源造轮子必备技术，否则你做完的轮子如何让别人使用难道是U盘拷贝？
面试题我面字节的时候就问到了这个
增加个人IP 让更多的人知道你的技术能力和贡献

npm adduser
首先先检查一下是否是npm源然后创建一个npm账号

创建完成之后使用npm login 登录账号

登录完成之后使用npm publish 发布npm包

发布成功 如果出现403说明包名被占用了
```

## npm搭建私服

```sh
构建npm私服
构建私服有什么收益吗？

可以离线使用，你可以将npm私服部署到内网集群，这样离线也可以访问私有的包。
提高包的安全性，使用私有的npm仓库可以更好的管理你的包，避免在使用公共的npm包的时候出现漏洞。
提高包的下载速度，使用私有 npm 仓库，你可以将经常使用的 npm 包缓存到本地，从而显著提高包的下载速度，减少依赖包的下载时间。这对于团队内部开发和持续集成、部署等场景非常有用

如何搭建npm 私服
verdaccio.org/zh-CN/
Verdaccio 是可以帮我们快速构建npm私服的一个工具


npm install verdaccio -g

verdaccio 直接运行即可

#创建账号
npm adduser --registry http://localhost:4873/
# 账号 密码 邮箱

# 发布npm
npm publish --registry http://localhost:4873/

#指定开启端口 默认 4873
verdaccio --listen 9999

# 指定安装源
npm install --registry http://localhost:4873

# 从本地仓库删除包
npm unpublish <package-name> --registry http://localhost:4873

其他配置文件项:https://verdaccio.org/zh-cn/docs/configuration/
```

## 模块化

Nodejs 模块化规范遵循两套一 套 `CommonJS` 规范另一套 `esm` 规范

### commonjs规范

```js
-----------`引入模块`-----------

//五种模式
//1.引入自己编写的模块
//require('./test.js')
//2.引入第三方模块
//const md5 = require('md5')
//console.log(md5('123456'))//e10adc3949ba59abbe56e057f20f883e
//3.nodejs内置模块 fs http net os child process
// const fs=require('node:fs')//高版本nodejs node:fs 低版本fs
// console.log(fs)
//4.C++展 addon napi node-gyp .node
//5.引入json文件
// const data=require('./data.json')
// console.log(data,1)

-----------`导出模块`-----------
这里是test.js的内容
// const a = 1;
// console.log(123);

module.exports = {
  success: 1,
  error: 0,
  fn: () => {
    console.log(123);
  },
};

导出模块exports 和 module.exports
module.exports = {
  hello: function() {
    console.log('Hello, world!');
  }
};

如果不想导出对象直接导出值
module.exports = 123
```

### esm规范

引入模块  `import`  必须写在头部,不支持引入json文件

```js
需要将package.json里的 "type":"commonjs" 改成 "type":"module"

index.js文件

import obj from './test.js'
console.log(obj);


test.js文件
export default {
  success: 1,
  error: 0,
};


如果要引入json文件需要特殊处理 需要增加断言并且指定类型json node低版本不支持
import data from './data.json' assert { type: "json" };
console.log(data);
```



## Cjs 和 ESM 的区别

1. Cjs是基于运行时的同步加载，esm是基于编译时的异步加载
2. Cjs是可以修改值的，esm值并且不可修改（可读的）
3. Cjs不可以tree shaking，esm支持tree shaking
4. commonjs中顶层的this指向这个模块本身，而ES6中顶层this指向undefined



## 全局变量

在nodejs中使用global定义全局变量，定义的变量

`globalThis` 属性根据环境自动判断，在nodejs环境会自动切换成global ，浏览器环境自动切换window非常方便



index.js文件

```js
// 这样运行不了
require('./child.js')
global.name = 'index.js'

// 正常运行
global.name = 'index.js'
require('./child.js')
```



child.js文件

```js
console.log(global.name);
```



**`__dirname` `__filename `只能在cjs使用 esm规范没有这两个全局变量**

```js
__dirname
```

它表示当前模块的所在`目录`的绝对路径

```js
__filename
```

它表示当前模块`文件`的绝对路径，包括文件名和文件扩展名



process命令

1. `process.argv`: 这是一个包含命令行参数的数组。第一个元素是Node.js的执行路径，第二个元素是当前执行的JavaScript文件的路径，之后的元素是传递给脚本的命令行参数。
2. `process.env`: 这是一个包含当前环境变量的对象。您可以通过`process.env`访问并操作环境变量。
3. `process.cwd()`: 这个方法返回当前工作目录的路径。
4. `process.on(event, listener)`: 用于注册事件监听器。您可以使用`process.on`监听诸如`exit`、`uncaughtException`等事件，并在事件发生时执行相应的回调函数。
5. `process.exit([code])`: 用于退出当前的Node.js进程。您可以提供一个可选的退出码作为参数。
6. `process.pid`: 这个属性返回当前进程的PID（进程ID）。

## CSR SSR SEO

```sh
npm i jsdom
```

`jsdom` 是一个模拟浏览器环境的库，可以在 Node.js 中使用 DOM API

```js
const fs = require("node:fs");
const { JSDOM } = require("jsdom");
const root = new JSDOM(`
    <!DOCTYPE HTML>
    <html>
    <head></head>
    <body>
        <div id='app'></div>
    </body>
    </html>
    `);

const window = root.window;
const document = window.document;

fetch("https://api.thecatapi.com/v1/images/search?limit=10&page=1")
  .then((res) => res.json())
  .then((data) => {
    const app = document.getElementById("app");
    data.forEach((item) => {
      const img = document.createElement("img");
      img.src = item.url;
      img.style.width = "200px";
      img.style.height = "200px";
      app.appendChild(img);
    });
    fs.writeFileSync("./index.html", root.serialize());
  });
```



上面的操作属于SSR  `（Server-Side Rendering）` 服务端渲染请求数据和拼装都在服务端完成，而我们的Vue,react 等框架这里不谈(nuxtjs,nextjs)，是在客户端完成渲染拼接的属于CSR `（Client-Side Rendering）` 客户端渲染

CSR 和 SSR 区别

1. 页面加载方式：
   - CSR：在 CSR 中，服务器返回一个初始的 HTML 页面，然后浏览器下载并执行 JavaScript 文件，JavaScript 负责动态生成并更新页面内容。这意味着初始页面加载时，内容较少，页面结构和样式可能存在一定的延迟。
   - SSR：在 SSR 中，服务器在返回给浏览器之前，会预先在服务器端生成完整的 HTML 页面，包含了初始的页面内容。浏览器接收到的是已经渲染好的 HTML 页面，因此初始加载的速度较快。
2. 内容生成和渲染：
   - CSR：在 CSR 中，页面的内容生成和渲染是由客户端的 JavaScript 脚本负责的。当数据变化时，JavaScript 会重新生成并更新 DOM，从而实现内容的动态变化。这种方式使得前端开发更加灵活，可以创建复杂的交互和动画效果。
   - SSR：在 SSR 中，服务器在渲染页面时会执行应用程序的代码，并生成最终的 HTML 页面。这意味着页面的初始内容是由服务器生成的，对于一些静态或少变的内容，可以提供更好的首次加载性能。
3. 用户交互和体验：
   - CSR：在 CSR 中，一旦初始页面加载完成，后续的用户交互通常是通过 AJAX 或 WebSocket 与服务器进行数据交互，然后通过 JavaScript 更新页面内容。这种方式可以提供更快的页面切换和响应速度，但对于搜索引擎爬虫和 SEO（搜索引擎优化）来说，可能需要一些额外的处理。
   - SSR：在 SSR 中，由于页面的初始内容是由服务器生成的，因此用户交互可以直接在服务器上执行，然后服务器返回更新后的页面。这样可以提供更好的首次加载性能和对搜索引擎友好的内容。

SEO   `（Search Engine Optimization，搜索引擎优化）`

## path

### path.basename

`path.basename()` 方法返回的是给定路径中的最后一部分

在posix处理windows路径

```js
path.basename('C:\temp\myfile.html');
// 返回: 'C:\temp\myfile.html'
```

结果返回的并不对 应该返回 myfile.html

如果要在posix系统处理windows的路径需要调用对应操作系统的方法应该修改为

```js
path.win32.basename('C:\temp\myfile.html');
```

### path.dirname

这个API和basename正好互补

```js
ath.dirname('/aaaa/bbbb/cccc/index.html')
```

dirname API 返回  /aaaa/bbbb/cccc  除了最后一个路径的其他路径。

basename API 返回 最后一个路径 index.html

### path.extname

这个API 用来返回扩展名例如/bbb/ccc/file.txt 返回就是.txt

```js
path.extname('/aaaa/bbbb/cccc/index.html.ccc.ddd.aaa')
//.aaa
如果有多个 . 返回最后一个 如果没有扩展名返回空
```

### path.join

这个API 主要是用来拼接路径的

```js
path.join('/foo','/cxk','/ikun')
// /foo/cxk/ikun
```

可以支持 .. ./ ../操作符

```js
path.join('/foo','/cxk','/ikun','../')
// /foo/cxk/
```

### path.resolve

用于将相对路径解析并且返回`绝对路径`

如果传入了多个绝对路径 它将返回最右边的绝对路径

```js
path.resolve('/aaa','/bbb','/ccc')
//   /ccc
```

传入绝对路径 + 相对路径

```js
path.resolve(__dirname,'./index.js')
//  /User/xiaoman/DeskTop/node/index.js
```

如果只传入相对路径

```js
path.resolve('./index.js')
// 返回工作目录 + index.js
```

### path.parse 和 path.format

path.format 和 path.parse 正好互补

`parse`

用于解析文件路径。它接受一个路径字符串作为输入，并返回一个包含路径各个组成部分的对象

```js
path.parse('/home/user/dir/file.txt')

{
  root: '/',
  dir: '/home/user/dir',
  base: 'file.txt',
  ext: '.txt',
  name: 'file'
}
```

format 正好相反 在把对象转回字符串

```js
path.format({
    root: '/',
    dir: '/home/user/documents',
    base: 'file.txt',
    ext: '.txt',
    name: 'file'
 })
// /home/user/dir/file.txt
```

## OS

```js
var os = require("node:os")
```

| 序号 |        API        | 作用                                                         |
| :--: | :---------------: | :----------------------------------------------------------- |
|  1   |   **os.type()**   | 它在 Linux 上返回 Linux，在 macOS 上返回 Darwin，在 Windows 上返回 Windows_NT |
|  2   | **os.platform()** | 返回标识为其编译 Node.js 二进制文件的操作系统平台的字符串。 该值在编译时设置。 可能的值为 aix、darwin、freebsd、linux、openbsd、sunos、以及 win32 |
|  3   | **os.release()**  | 返回操作系统的版本例如10.xxxx win10                          |
|  4   | **os.homedir()**  | 返回用户目录 例如c:\user\xiaoman 原理就是 windows `echo %USERPROFILE%`  posix $HOME |
|  5   |   **os.arch()**   | 返回cpu的架构 可能的值为arm、arm64、ia32、mips、mipsel、ppc、ppc64、s390、s390x、以及 x64 |

**获取CPU的线程以及详细信息**

```js
const os = require('node:os')
os.cpus()
```

`model`: 表示CPU的型号信息，其中 "Intel(R) Core(TM) i7 CPU 860 @ 2.80GHz" 是一种具体的型号描述。

`speed`: 表示CPU的时钟速度，以MHz或GHz为单位。在这种情况下，速度为 2926 MHz 或 2.926 GHz。

`times`: 是一个包含CPU使用时间的对象，其中包含以下属性：

- `user`: 表示CPU被用户程序使用的时间（以毫秒为单位）。
- `nice`: 表示CPU被优先级较低的用户程序使用的时间（以毫秒为单位）。
- `sys`: 表示CPU被系统内核使用的时间（以毫秒为单位）。
- `idle`: 表示CPU处于空闲状态的时间（以毫秒为单位）。
- `irq`: 表示CPU被硬件中断处理程序使用的时间（以毫秒为单位）。

**获取网络信息**

```js
const os = require('node:os')
os.networkInterfaces()
```

- `address`: 表示本地回环接口的IP地址，这里是 `'127.0.0.1'`。
- `netmask`: 表示本地回环接口的子网掩码，这里是 `'255.0.0.0'`。
- `family`: 表示地址族（address family），这里是 `'IPv4'`，表示IPv4地址。
- `mac`: 表示本地回环接口的MAC地址，这里是 `'00:00:00:00:00:00'`。请注意，本地回环接口通常不涉及硬件，因此MAC地址通常为全零。
- `internal`: 表示本地回环接口是否是内部接口，这里是 `true`，表示它是一个内部接口。
- `cidr`: 表示本地回环接口的CIDR表示法，即网络地址和子网掩码的组合，这里是 `'127.0.0.1/8'`，表示整个 `127.0.0.0` 网络。

## process

`process` 是Nodejs操作当前进程和控制当前进程的API，并且是挂载到globalThis下面的全局API

### process.arch

返回操作系统 CPU 架构 跟我们之前讲的os.arch 一样 `'arm'`、`'arm64'`、`'ia32'`、`'mips'`、`'mipsel'`、`'ppc'`、`'ppc64'`、`'s390'`、`'s390x'`、以及 `'x64'`

### process.cwd()

返回当前的工作目录，例如在 F:\project\node> 执行的脚本就返回这个目录也可以和path拼接代替__dirname使用

### process.argv

获取执行进程后面的参数 返回是一个数组 后面我们讲到命令行交互工具的时候会很有用，各种cli脚手架也是使用这种方式接受配置参数例如`webpack`

### process.memoryUsage

用于获取当前进程的内存使用情况。该方法返回一个对象，其中包含了各种内存使用指标，如 rss（Resident Set Size，常驻集大小）、heapTotal（堆区总大小）、heapUsed（已用堆大小）和 external（外部内存使用量）等

### process.exit()

调用 `process.exit()` 将强制进程尽快退出，即使仍有未完全完成的异步操作挂起

### process.kill

与exit类似，kill用来杀死一个进程，接受一个参数进程id可以通过process.pid 获取

```js
process.kill(process.pid)
```

### process.env

用于读取操作系统所有的环境变量，也可以修改和查询环境变量。

**修改 注意修改并不会真正影响操作系统的变量，而是只在当前线程生效，线程结束便释放**

## child_process 子进程

**创建子进程**

Nodejs创建子进程共有7个API Sync同步API，不加是异步API

1. spawn  执行命令
2. exec   执行命令
3. execFile   执行可执行文件
4. fork   创建node子进程
5. execSync 执行命令 同步执行
6. execFileSync 执行可执行文件 同步执行
7. spawnSync 执行命令 同步执行



**获取nodejs 版本号**

```js
const {
  exec,
  execSync,
  spawn,
  spawnSync,
  execFile,
  execFileSync,
  fork,
} = require("child_process");


 exec('node -v',(err,stdout,stderr)=>{
    if(err){
        return  err
    }
    console.log(stdout.toString())
 })
```



**execSync**

获取node版本号 如果要执行单次shell命令execSync方便一些 options同上

```js
const nodeVersion  = execSync('node -v')
console.log(nodeVersion.toString("utf-8"))
```

打开谷歌浏览器 使用exec可以打开一些软件例如 wx 谷歌 qq音乐等 以下会打开百度并且进入`无痕模式`

```js
execSync("start chrome http://www.baidu.com --incognito")
execSync(' "D:\\Program Files\\Soda Music\\SodaMusicLauncher.exe" ')
```



**execFile**

execFile 适合执行可执行文件，例如执行一个node脚本，或者shell文件，windows可以编写cmd脚本，posix，可以编写sh脚本

bat.cmd文件 创建一个文件夹mkdir 进入目录 写入一个文件test.js 最后执行

```cmd
echo '开始'

mkdir test 

cd ./test

echo console.log("test1232131") >test.js

echo '结束'

node test.js
```

使用execFile 执行这个

```js
const path = require("node:path");
execFile(path.resolve(process.cwd(),'./bat.cmd'),{ shell: true },(err,stdout)=>{
    console.log(stdout.toString())
})
```



**spawn**

spawn 用于执行一些实时获取的信息因为spawn返回的是流边执行边返回，exec是返回一个完整的buffer，buffer的大小是200k，如果超出会报错，而spawn是无上限的。

spawn在执行完成后会抛出close事件监听，并返回状态码，通过状态码可以知道子进程是否顺利执行。exec只能通过返回的buffer去识别完成状态，识别起来较为麻烦

```js
// 命令      参数  options配置
const {stdout} = spawn('netstat',['-an'],{options配置})

//返回的数据用data事件接受
stdout.on('data',(steram)=>{
    console.log(steram.toString())
})

stdout.on('close',(steram)=>{
  console.log('结束了')
})
```



**options 配置项**

```txt
cwd <string> 子进程的当前工作目录。
env <Object> 环境变量键值对。
encoding <string> 默认为 'utf8'。
shell <string> 用于执行命令的 shell。 在 UNIX 上默认为 '/bin/sh'，在 Windows 上默认为 process.env.ComSpec。 详见 Shell Requirements 与 Default Windows Shell。
timeout <number> 默认为 0。
maxBuffer <number> stdout 或 stderr 允许的最大字节数。 默认为 200*1024。 如果超过限制，则子进程会被终止。 查看警告： maxBuffer and Unicode。
killSignal <string> | <integer> 默认为 'SIGTERM'。
uid <number> 设置该进程的用户标识。（详见 setuid(2)）
gid <number> 设置该进程的组标识。（详见 setgid(2)）
```



**fork**

场景适合大量的计算，或者容易阻塞主进程操作的一些代码，就适合开发fork

index.js

```js
const {fork} = require('child_process')

const testProcess = fork('./test.js')

testProcess.send('我是主进程')

testProcess.on("message",(data)=>{
    console.log('我是主进程接受消息111：',data)
})
```

test.js

```js
process.on('message',(data)=>{

    console.log('子进程接受消息：',data)
})

process.send('我是子进程')
```



## ffmpeg

FFmpeg 是一个开源的跨平台多媒体处理工具，可以用于处理音频、视频和多媒体流。它提供了一组强大的命令行工具和库，可以进行视频转码、视频剪辑、音频提取、音视频合并、流媒体传输等操作。

安装路径 : https://ffmpeg.p2hp.com/download.html

1、简单的demo 视频转gif `-i` 表示输入的意思

```js
const {execSync} = require('child_process')
execSync(`ffmpeg -i test.mp4 test.gif`,{stdio:'inherit'})
```

2、添加水印

-vf 就是video filter

drawtext 添加文字 fontsize 大小 xy垂直水平方向 fontcolor 颜色 text 水印文案 `全部小写`

```js
const {execSync} = require('child_process')

execSync(`ffmpeg -i test.mp4 -vf drawtext=text="XMZS":fontsize=30:fontcolor=white:x=10:y=10 test2.mp4`,{stdio:'inherit'})
```

3、视频裁剪 + 控制大小

-ss 起始时间

-to 结束事件

> ss写在 -i的前面可能会导致精度问题，因为视频还没解析就跳转到了相关位置，但是解析速度快

> ss写在 -i后面精度没问题，但是解析速度会变慢

```js
const {execSync} = require('child_process')

execSync(`ffmpeg -ss 10 -to 20 -i test.mp4  test3.mp4`,{stdio:'inherit'})
```

4、提取视频的音频

```js
const {execSync} = require('child_process')
execSync(`ffmpeg -i test.mp4 test.mp3`,{stdio:'inherit'})
```

5、去掉水印

w h 宽高 xy 垂直 水平坐标 delogo使用的过滤参数删除水印

```js
const {execSync} = require('child_process')

execSync(`ffmpeg -i  test2.mp4 -vf delogo=w=120:h=30:x=10:y=10 test3.mp4`,{stdio:'inherit'})
```



## events

Node.js 核心 API 都是采用异步事件驱动架构，简单来说就是通过有效的方法来监听事件状态的变化，并在变化的时候做出相应的动作。

```mermaid
sequenceDiagram
    participant 发布者
    participant 调度中心
    participant 订阅者test1
    participant 订阅者test2

    订阅者test1->>调度中心: 订阅test1主题
    订阅者test2->>调度中心: 订阅test2主题
    
    发布者->>调度中心: 发布test1主题消息
    调度中心->>订阅者test1: 分发test1消息
    
    发布者->>调度中心: 发布test2主题消息
    调度中心->>订阅者test2: 分发test2消息
```

**监听消息数量默认是10个**

```js
const evnentEmitter = require('events')

// 发布订阅模式 off on emit once
const event = new evnentEmitter()

//订阅一个事件
event.on('test', (data)=>{
    console.log(data);
})

//发布
event.emit('test','哇哈哈哈哈') //派发事件
```



只想监听一次 once 即使`emit`派发多次也只触发一次---`once`

```js
const evnentEmitter = require('events')

const event = new evnentEmitter()
// 如何解除限制 调用 setMaxListeners 传入数量
event.setMaxListeners(20)
//订阅一个事件
event.once('test', (data)=>{
    console.log(data);
})

//发布
event.emit('test','哇哈哈哈哈1') //派发事件
event.emit('test','哇哈哈哈哈2') //派发事件
```



如何取消侦听 --- `off`

```js
const evnentEmitter = require('events')

const event = new evnentEmitter()

const fn = (msg) => {
    console.log(msg);
}

event.on('test', fn)
// event.off('test', fn)

//发布
event.emit('test','哇哈哈哈哈1') //派发事件
event.emit('test','哇哈哈哈哈2') //派发事件
```

## util

例如我们之前讲的  `exec`

获取Node版本

```js
import { exec } from 'node:child_process'
exec('node -v', (err,stdout)=>{
   if(err){
      return err
   }
   console.log(stdout)
})
```

以上就是常规写法

我们使用util的`promisify` 改为promise 风格 Promiseify 接受 `original`一个函数体

```js
import util from "node:util";
import { exec } from "node:child_process";
import { stderr } from "node:process";

exec("node -v", (err, stdout, stderr) => {
  if (err) {
    return err;
  }
  console.log(stdout);
});


import util from "node:util";
import { exec } from "node:child_process";
const execPromise = util.promisify(exec) //返回一个新的函数

//如果返回多个参数res对象 如果返回一个参数 就直接返回对象
execPromise('node -v').then(res=>{
    console.log(res);
}).catch(err=>{
    console.log(err);
})
```

### 剖析promiseify如何实现的

1、第一步Promiseify是返回一个新的函数

```js
const promiseify = () => {
   return () => {

  }
}
```

2、promiseify接受一个函数，并且在返回的函数才接受真正的参数，然后返回一个promise

```js
const promiseify = (original) => {
   return (...args) => {
     return new Promise((resolve,reject)=>{
        
     })
  }
}
```

3、调用真正的函数，将参数透传给original，如果失败了就reject，如果成功了，就返回resolve，如果有多个返回一个对象。

```js

const promisify = (fn) =>{
    return (...args) =>{
        return new Promise((resolve,reject)=>{
            fn(...args, (err, ...values)=>{
                if(err){
                    reject(err)
                }
                if(values && values.length >1){
                    let obj = {}
                    for (let key in values) {
                        obj[key] = values[key]
                    }
                    resolve(obj)
                }else{
                    resolve(values[0])
                }
            })
        })
    }
}

const execPromise = promisify(exec)

execPromise('node -v').then(res=>{
    console.log(res, 'res');
}).catch(err=>{
    console.log(err, 'err');
})
```

### util.callbackify

```js
const fn = (type) => {
    if(type == 1) {
        return Promise.resolve('success')
    }else{
        return Promise.reject('error')
    }
}

const callback = util.callbackify(fn)

callback(2,(err,value)=>{
    console.log(err,value);
})

--------------------------------------------------------------------------------
//自己写一个function
const callbackify = (fn) =>{
    return (...args) =>{
        let callback = args.pop()
        fn(...args).then(res =>{
            callback(null, res)
        }).catch(err=>{
            callback(err)
        })
    }
}

const fn = (type) => {
    if(type == 1) {
        return Promise.resolve('success')
    }else{
        return Promise.reject('error')
    }
}

const callback = callbackify(fn)

callback(1,(err,value)=>{
    console.log(err,value);
})
```



### util.format

- `%s`: `String` 将用于转换除 `BigInt`、`Object` 和 `-0` 之外的所有值。 `BigInt` 值将用 `n` 表示，没有用户定义的 `toString` 函数的对象使用具有选项 `{ depth: 0, colors: false, compact: 3 }` 的 `util.inspect()` 进行检查。
- `%d`: `Number` 将用于转换除 `BigInt` 和 `Symbol` 之外的所有值。
- `%i`: `parseInt(value, 10)` 用于除 `BigInt` 和 `Symbol` 之外的所有值。
- `%f`: `parseFloat(value)` 用于除 `Symbol` 之外的所有值。
- `%j`: JSON。 如果参数包含循环引用，则替换为字符串 `'[Circular]'`。
- `%o`: `Object`. 具有通用 JavaScript 对象格式的对象的字符串表示形式。 类似于具有选项 `{ showHidden: true, showProxy: true }` 的 `util.inspect()`。 这将显示完整的对象，包括不可枚举的属性和代理。
- `%O`: `Object`. 具有通用 JavaScript 对象格式的对象的字符串表示形式。 类似于没有选项的 `util.inspect()`。 这将显示完整的对象，但不包括不可枚举的属性和代理。
- `%c`: `CSS`. 此说明符被忽略，将跳过任何传入的 CSS。
- `%%`: 单个百分号 (`'%'`)。 这不消费参数。

```js
util.format('%s-----%s %s/%s','foo','bar','xm','zs')
```

## pngquant

`pngquant`   是一个用于压缩 PNG 图像文件的工具。它可以显著减小 PNG 文件的大小，同时保持图像质量和透明度。通过减小文件大小，可以提高网页加载速度，并节省存储空间。`pngquant`   提供命令行接口和库，可轻松集成到各种应用程序和脚本中。

网址：http://pngquant.com/

**Nodejs 中 调用pngquant**

我们同样还是可以用`exec`命令调用

```js
import { exec } from 'child_process'
exec('pngquant 73kb.png --output test.png')
```

73kb 压缩完 之后 22kb

```js
import { exec } from 'child_process'
exec('pngquant 73kb.png --quality=82 --output test.png')
```

quality表示图片质量0-100值越大图片越大效果越好

```js
import { exec } from 'child_process'
exec('pngquant 73kb.png --speed=1 --quality=82 --output test.png')
```

- `--speed=1`: 最慢的速度，产生最高质量的输出图像。
- `--speed=10`: 最快的速度，但可能导致输出图像质量稍微降低。



上面方法不行使用  `npm install pngquant-bin`

```js
import { execFile } from 'child_process';
import pngquant from 'pngquant-bin';

console.log('使用 pngquant 路径:', pngquant); // 确认路径

execFile(pngquant, ['80', '80kb.png', '--output', 'test.png'], {
  cwd: __dirname
}, (error) => {
  if (error) {
    console.error('压缩失败:', error);
    return;
  }
  console.log('✅ 压缩成功！');
});
```



## fs

fs模块是文件系统模块

1. 读取文件  readFile flag
2. 可读流 createReadStream
3. 创建文件夹 recursive 递归
4. 删除rm
5. 重命名 renameSync
6. 临听文件变化 watch
7. 源码 libuv
8. 注意事项事件循环 setImmediate

### 读取文件

```js
const fs = require("node:fs");
const fs2 = require("node:fs/promises");

// 不加Sync就是异步的
fs.readFile(
  "./index.txt",
  {
    encoding: "utf-8",
    flag: "r",
  },
  (err, data) => {
    if (err) throw err;
    console.log(data);
  }
);

//同步方式阻塞下面的代码
let result = fs.readFileSync("./index.txt");
console.log(result.toString("utf-8"));
console.log('test');

// promise方法
fs2.readFile('./index.txt').then(result =>{
    console.log(result.toString())
})
```

### 可读流

```js
const fs = require("node:fs");

const readStream = fs.createReadStream('./index.txt',{
    encoding:"utf8"
})

readStream.on('data',(chunk)=>{
    console.log(chunk.toString())
})

readStream.on('end',()=>{
    console.log('结束，读取完成')
})
```

### 创建文件夹

```js
// 创建文件夹 如果开启 recursive 可以递归创建多个文件夹
fs.mkdir('path/test/ccc', { recursive: true },(err)=>{

})
```

### 删除文件夹

```js
// 删除文件夹 如果开启recursive 递归删除全部文件夹
fs.rm('path', { recursive: true },(err)=>{

})
```

### 重命名文件

```js
// 重命名文件 第一个参数原始名称 第二个参数新的名称
fs.renameSync('./index.txt','./index2.txt')
```

### 临听文件变化

```js
// 监听文件的变化 返回监听的事件如change,和监听的内容filename

fs.watch('./index.txt',(event,filename)=>{
    console.log(event,filename)
})
```

### 注意事项

为什么先走setImmediate 呢，而不是fs

Node.js 读取文件的时候是使用libuv进行调度的

而setImmediate是由V8进行调度的

文件读取完成后 libuv 才会将 fs的结果 推入V8的队列

```js
const fs = require('node:fs')

fs.readFile('./index.txt', {
    encoding: 'utf-8',
    flag: 'r'
}, (err, dataStr) => {
    if (err) throw err
    console.log('fs')
})

setImmediate(() => {
    console.log('setImmediate')
})
```

### 写入内容

```js
const fs = require("node:fs");

fs.writeFileSync('./index.txt','java之父 \n余圣军')
```

- `'a'`: 打开文件进行追加。 如果文件不存在，则创建该文件。
- `'ax'`: 类似于 `'a'` 但如果路径存在则失败。
- `'a+'`: 打开文件进行读取和追加。 如果文件不存在，则创建该文件。
- `'ax+'`: 类似于 `'a+'` 但如果路径存在则失败。
- `'as'`: 以同步模式打开文件进行追加。 如果文件不存在，则创建该文件。
- `'as+'`: 以同步模式打开文件进行读取和追加。 如果文件不存在，则创建该文件。
- `'r'`: 打开文件进行读取。 如果文件不存在，则会发生异常。
- `'r+'`: 打开文件进行读写。 如果文件不存在，则会发生异常。
- `'rs+'`: 以同步模式打开文件进行读写。 指示操作系统绕过本地文件系统缓存。
- 这主要用于在 NFS 挂载上打开文件，因为它允许跳过可能过时的本地缓存。 它对 I/O 性能有非常实际的影响，因此除非需要，否则不建议使用此标志。
- 这不会将 `fs.open()` 或 `fsPromises.open()` 变成同步阻塞调用。 如果需要同步操作，应该使用类似 `fs.openSync()` 的东西。
- `'w'`: 打开文件进行写入。 创建（如果它不存在）或截断（如果它存在）该文件。
- `'wx'`: 类似于 `'w'` 但如果路径存在则失败。
- `'w+'`: 打开文件进行读写。 创建（如果它不存在）或截断（如果它存在）该文件。
- `'wx+'`: 类似于 `'w+'` 但如果路径存在则失败。

### 追加内容

第一种方式

```js
const fs = require("node:fs");

fs.writeFileSync('index.txt', '\nvue之父\n鱿鱼须',{
    flag: 'a'
})
```

第二种方式

```js
const fs = require('node:fs')

fs.appendFileSync('index.txt', '\nunshift创始人\n麒麟哥')
```

### 可写流

```js
const fs = require("node:fs");

let verse = [
    '待到秋来九月八',
    '我花开后百花杀',
    '冲天香阵透长安',
    '满城尽带黄金甲'
]

let writeStream = fs.createWriteStream('./index.txt')

verse.forEach(item => {
    writeStream.write(item + '\n')
})

writeStream.end()

writeStream.on('finish',()=>{
    console.log('写入完成')
})
```

### 硬链接 和 软连接

```js
fs.linkSync('./index.txt', './index2.txt') //硬链接

fs.symlinkSync('./index.txt', './index3.txt' ,"file") //软连接
```

硬链接的作用和用途如下：

1. 文件共享：硬链接允许多个文件名指向同一个文件，这样可以在不同的位置使用不同的文件名引用相同的内容。这样的共享文件可以节省存储空间，并且在多个位置对文件的修改会反映在所有引用文件上。
2. 文件备份：通过创建硬链接，可以在不复制文件的情况下创建文件的备份。如果原始文件发生更改，备份文件也会自动更新。这样可以节省磁盘空间，并确保备份文件与原始文件保持同步。
3. 文件重命名：通过创建硬链接，可以为文件创建一个新的文件名，而无需复制或移动文件。这对于需要更改文件名但保持相同内容和属性的场景非常有用。

软链接的一些特点和用途如下：

1. 软链接可以创建指向文件或目录的引用。这使得你可以在不复制或移动文件的情况下引用它们，并在不同位置使用不同的文件名访问相同的内容。
2. 软链接可以用于创建快捷方式或别名，使得你可以通过一个简短或易记的路径来访问复杂或深层次的目录结构。
3. 软链接可以用于解决文件或目录的位置变化问题。如果目标文件或目录被移动或重命名，只需更新软链接的目标路径即可，而不需要修改引用该文件或目录的其他代码。

## crypto

### 对称加密

```js
const crypto = require('node:crypto');

// 生成一个随机的 16 字节的初始化向量 (IV)
const iv = Buffer.from(crypto.randomBytes(16));

// 生成一个随机的 32 字节的密钥
const key = crypto.randomBytes(32);

// 创建加密实例，使用 AES-256-CBC 算法，提供密钥和初始化向量
const cipher = crypto.createCipheriv("aes-256-cbc", key, iv);

// 对输入数据进行加密，并输出加密结果的十六进制表示
cipher.update("小满zs", "utf-8", "hex");
const result = cipher.final("hex");
console.log("Result", result);

// 解密
const de = crypto.createDecipheriv("aes-256-cbc", key, iv);
de.update(result, "hex");
const decrypted = de.final("utf-8");

console.log("Decrypted:", decrypted);
```

### 非对称加密

```js
const crypto = require('node:crypto')
// 生成 RSA 密钥对
const { privateKey, publicKey } = crypto.generateKeyPairSync('rsa', {
  modulusLength: 2048,
});

// 要加密的数据
const text = '小满zs';

// 使用公钥进行加密
const encrypted = crypto.publicEncrypt(publicKey, Buffer.from(text, 'utf-8'));

console.log(encrypted.toString('hex'));

// 使用私钥进行解密
const decrypted = crypto.privateDecrypt(privateKey, encrypted);

console.log(decrypted.toString());
```

### 哈希函数

哈希函数具有以下特点：

1. 固定长度输出：不论输入数据的大小，哈希函数的输出长度是固定的。例如，常见的哈希函数如 MD5 和 SHA-256 生成的哈希值长度分别为 128 位和 256 位。
2. 不可逆性：哈希函数是单向的，意味着从哈希值推导出原始输入数据是非常困难的，几乎不可能。即使输入数据发生微小的变化，其哈希值也会完全不同。
3. 唯一性：哈希函数应该具有较低的碰撞概率，即不同的输入数据生成相同的哈希值的可能性应该非常小。这有助于确保哈希值能够唯一地标识输入数据。

使用场景

1. 我们可以避免密码明文传输 使用md5加密或者sha256
2. 验证文件完整性，读取文件内容生成md5 如果前端上传的md5和后端的读取文件内部的md5匹配说明文件是完整的

```js
const crypto = require('node:crypto');

// 要计算哈希的数据
let text = '123456';

// 创建哈希对象，并使用 MD5 算法
const hash = crypto.createHash('md5');

// 更新哈希对象的数据
hash.update(text);

// 计算哈希值，并以十六进制字符串形式输出
const hashValue = hash.digest('hex');

console.log('Text:', text);
console.log('Hash:', hashValue);
```

## 脚手架

编写自己的脚手架是指创建一个定制化的工具，用于快速生成项目的基础结构和代码文件，以及提供一些常用的命令和功能。通过编写自己的脚手架，你可以定义项目的目录结构、文件模板，管理项目的依赖项，生成代码片段，以及提供命令行接口等功能

1. 项目结构：脚手架定义了项目的目录结构，包括源代码、配置文件、静态资源等。
2. 文件模板：脚手架提供了一些预定义的文件模板，如HTML模板、样式表、配置文件等，以加快开发者创建新文件的速度。
3. 命令行接口：脚手架通常提供一个命令行接口，通过输入命令和参数，开发者可以执行各种任务，如创建新项目、生成代码文件、运行测试等。
4. 依赖管理：脚手架可以帮助开发者管理项目的依赖项，自动安装和配置所需的库和工具。
5. 代码生成：脚手架可以生成常见的代码结构，如组件、模块、路由等，以提高开发效率。
6. 配置管理：脚手架可以提供一些默认的配置选项，并允许开发者根据需要进行自定义配置。

### 工具介绍

哪个前端不想拥有自己的一套脚手架，在这一章节你会学到非常多的第三方库，如

- **`commander`**

> Commander 是一个用于构建命令行工具的 npm 库。它提供了一种简单而直观的方式来创建命令行接口，并处理命令行参数和选项。使用 Commander，你可以轻松定义命令、子命令、选项和帮助信息。它还可以处理命令行的交互，使用户能够与你的命令行工具进行交互

- **`inquirer`**

> Inquirer 是一个强大的命令行交互工具，用于与用户进行交互和收集信息。它提供了各种丰富的交互式提示（如输入框、选择列表、确认框等），可以帮助你构建灵活的命令行界面。通过 Inquirer，你可以向用户提出问题，获取用户的输入，并根据用户的回答采取相应的操作。

- **`ora`**

> Ora 是一个用于在命令行界面显示加载动画的 npm 库。它可以帮助你在执行耗时的任务时提供一个友好的加载状态提示。Ora 提供了一系列自定义的加载动画，如旋转器、进度条等，你可以根据需要选择合适的加载动画效果，并在任务执行期间显示对应的加载状态。

- **`download-git-repo`**

> Download-git-repo 是一个用于下载 Git 仓库的 npm 库。它提供了一个简单的接口，可以方便地从远程 Git 仓库中下载项目代码。你可以指定要下载的仓库和目标目录，并可选择指定分支或标签。Download-git-repo 支持从各种 Git 托管平台（如 GitHub、GitLab、Bitbucket 等）下载代码。

index.js

```js
#!/usr/bin/env node
//告诉操作系统我执行自定义命令的时候 你帮我用node去执行 这个文件

import { program } from "commander";
import fs from "node:fs";
import inquirer from "inquirer";
import { checkPath, downloadTemp } from "./utils.js";
let json = fs.readFileSync("./package.json");
json = JSON.parse(json);

program.version(json.version);

program
  .command("create <projectName>")
  .alias("c")
  .description("创建项目")
  .action((projectName) => {
    inquirer
      .prompt([
        {
          type: "input", //输入 input 输入 confirm 确认框 list 选择框 checkbox
          name: "projectName", //返回值的key
          message: "请输入项目名称", //描述
          default: projectName, //默认值
        },
        {
          type: "confirm", //输入 input 输入 confirm 确认框 list 选择框 checkbox
          name: "isTs", //返回值的key
          message: "是否选用typeScript模板",
        },
      ])
      .then((res) => {
        if (checkPath(res.projectName)) {
          console.log("文件夹已存在");
          return;
        }
        if (res.isTs) {
          downloadTemp('ts',res.projectName)
        } else {
          downloadTemp('js',res.projectName)
        }
      });
  });

program.parse(process.argv);
```

utils.js

```js
import fs from "node:fs";
import download from "download-git-repo";
import ora from "ora";
const spinner = ora("下载中...");

//检查路径
export const checkPath = (path) => {
  if (fs.existsSync(path)) {
    return true;
  } else {
    return false;
  }
};

export const downloadTemp = (branch, project) => {
  spinner.start();
  return new Promise((resolve, reject) => {
    download(
      `direct:https://gitee.com/chinafaker/vue-template.git#${branch}`,
      project,
      { clone: true },
      function (err) {
        if (err) {
          reject(err);
          console.log(err);
        }
        resolve();
        spinner.succeed("下载完成");
      }
    );
  });
};
```

package.json

```json
 "type": "module", //使用import需要设置这个
 "bin": {
    "vue-cli": "src/index.js"
  },
```

用于生成软连接挂载到全局，便可以全局执行vue-cli 这个命令，配置完成之后 需要执行

```sh
npm link
```

## Markdown 转 html

我们需要用到三个库实现

1. **EJS**：一款强大的JavaScript模板引擎，它可以帮助我们在HTML中嵌入动态内容。使用EJS，您可以轻松地将Markdown转换为美观的HTML页面。
2. **Marked**：一个流行的Markdown解析器和编译器，它可以将Markdown语法转换为HTML标记。Marked是一个功能强大且易于使用的库，它为您提供了丰富的选项和扩展功能，以满足各种转换需求。
3. **BrowserSync**：一个强大的开发工具，它可以帮助您实时预览和同步您的网页更改。当您对Markdown文件进行编辑并将其转换为HTML时，BrowserSync可以自动刷新您的浏览器，使您能够即时查看转换后的结果。

```sh
npm install ejs
npm install marked
npm install browser-sync
```

**template.ejs**---->初始化模板 到时候会转换成html代码

```ejs
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title><%= title %></title>
    <link rel="stylesheet" href="./index.css">
</head>
<body>
    <%- content %>
</body>
</html>
```

**marked**---->编写一个简易的md文档

```js
 ### 标题
 - test
```

**index.css**---->html代码有了 但是没有通用的markdown的通用css

```css
/* Markdown通用样式 */

/* 设置全局字体样式 */
body {
    font-family: Arial, sans-serif;
    font-size: 16px;
    line-height: 1.6;
    color: #333;
  }
  
  /* 设置标题样式 */
  h1,
  h2,
  h3,
  h4,
  h5,
  h6 {
    margin-top: 1.3em;
    margin-bottom: 0.6em;
    font-weight: bold;
  }
  
  h1 {
    font-size: 2.2em;
  }
  
  h2 {
    font-size: 1.8em;
  }
  
  h3 {
    font-size: 1.6em;
  }
  
  h4 {
    font-size: 1.4em;
  }
  
  h5 {
    font-size: 1.2em;
  }
  
  h6 {
    font-size: 1em;
  }
  
  /* 设置段落样式 */
  p {
    margin-bottom: 1.3em;
  }
  
  /* 设置链接样式 */
  a {
    color: #337ab7;
    text-decoration: none;
  }
  
  a:hover {
    text-decoration: underline;
  }
  
  /* 设置列表样式 */
  ul,
  ol {
    margin-top: 0;
    margin-bottom: 1.3em;
    padding-left: 2em;
  }
  
  /* 设置代码块样式 */
  pre {
    background-color: #f7f7f7;
    padding: 1em;
    border-radius: 4px;
    overflow: auto;
  }
  
  code {
    font-family: Consolas, Monaco, Courier, monospace;
    font-size: 0.9em;
    background-color: #f7f7f7;
    padding: 0.2em 0.4em;
    border-radius: 4px;
  }
  
  /* 设置引用样式 */
  blockquote {
    margin: 0;
    padding-left: 1em;
    border-left: 4px solid #ddd;
    color: #777;
  }
  
  /* 设置表格样式 */
  table {
    border-collapse: collapse;
    width: 100%;
    margin-bottom: 1.3em;
  }
  
  table th,
  table td {
    padding: 0.5em;
    border: 1px solid #ccc;
  }
  
  /* 添加一些额外的样式，如图片居中显示 */
  img {
    display: block;
    margin: 0 auto;
    max-width: 100%;
    height: auto;
  }
  
  /* 设置代码行号样式 */
  pre code .line-numbers {
    display: inline-block;
    width: 2em;
    padding-right: 1em;
    color: #999;
    text-align: right;
    user-select: none;
    pointer-events: none;
    border-right: 1px solid #ddd;
    margin-right: 0.5em;
  }
  
  /* 设置代码行样式 */
  pre code .line {
    display: block;
    padding-left: 1.5em;
  }
  
  /* 设置代码高亮样式 */
  pre code .line.highlighted {
    background-color: #f7f7f7;
  }
  
  /* 添加一些响应式样式，适应移动设备 */
  @media only screen and (max-width: 768px) {
    body {
      font-size: 14px;
      line-height: 1.5;
    }
    
    h1 {
      font-size: 1.8em;
    }
    
    h2 {
      font-size: 1.5em;
    }
    
    h3 {
      font-size: 1.3em;
    }
    
    h4 {
      font-size: 1.1em;
    }
    
    h5 {
      font-size: 1em;
    }
    
    h6 {
      font-size: 0.9em;
    }
    
    table {
      font-size: 14px;
    }
  }
```

index.js

```js
const ejs = require('ejs'); // 导入ejs库，用于渲染模板
const fs = require('node:fs'); // 导入fs模块，用于文件系统操作
const marked = require('marked'); // 导入marked库，用于将Markdown转换为HTML
const readme = fs.readFileSync('README.md'); // 读取README.md文件的内容
const browserSync = require('browser-sync'); // 导入browser-sync库，用于实时预览和同步浏览器
const openBrowser =  () => {
    const browser = browserSync.create()
    browser.init({
        server: {
            baseDir: './',
            index: 'index.html',
        }
    })
    return browser
}
ejs.renderFile('template.ejs', {
    content: marked.parse(readme.toString()),
    title:'markdown to html'
},(err,data)=>{
    if(err){
        console.log(err)
    }
    let writeStream = fs.createWriteStream('index.html')
    writeStream.write(data)
    writeStream.close()
    writeStream.on('finish',()=>{
        openBrowser()
    })
})
```

## zlib

`zlib` 模块的主要作用如下：

1. 数据压缩：使用 `zlib` 模块可以将数据以无损压缩算法（如 Deflate、Gzip）进行压缩，减少数据的大小。这在网络传输和磁盘存储中特别有用，可以节省带宽和存储空间。
2. 数据解压缩：`zlib` 模块还提供了对压缩数据的解压缩功能，可以还原压缩前的原始数据。
3. 流压缩：`zlib` 模块支持使用流（`Stream`）的方式进行数据的压缩和解压缩。这种方式使得可以对大型文件或网络数据流进行逐步处理，而不需要将整个数据加载到内存中。
4. 压缩格式支持：`zlib` 模块支持多种常见的压缩格式，如 Gzip 和 Deflate。这些格式在各种应用场景中广泛使用，例如 HTTP 响应的内容编码、文件压缩和解压缩等。



**压缩一个txt文件gzip**   index.txt     压缩完index.txt.gz

```js
// 引入所需的模块
const zlib = require('zlib'); // zlib 模块提供数据压缩和解压缩功能
const fs = require('node:fs'); // 引入 Node.js 的 fs 模块用于文件操作

// 创建可读流和可写流
const readStream = fs.createReadStream('index.txt'); // 创建可读流，读取名为 index.txt 的文件
const writeStream = fs.createWriteStream('index.txt.gz'); // 创建可写流，将压缩后的数据写入 index.txt.gz 文件

// 使用管道将可读流中的数据通过 Gzip 压缩，再通过管道传输到可写流中进行写入
readStream.pipe(zlib.createGzip()).pipe(writeStream)
```

**解压  gzip**

```js
const readStrem = fs.createReadStream('index.txt.gz')
const writeStrem = fs.createWriteStream('index2.txt')
readStrem.pipe(zlib.createGunzip()).pipe(writeStrem)
```

**无损压缩 deflate**   使用 createDeflate方法

```js
const readStream = fs.createReadStream('index.txt'); // 创建可读流，读取名为 index.txt 的文件
const writeStream = fs.createWriteStream('index.txt.deflate'); // 创建可写流，将压缩后的数据写入 index.txt.deflate 文件
readStream.pipe(zlib.createDeflate()).pipe(writeStream);
```

**解压  deflate**

```js
const readStream = fs.createReadStream('index.txt.deflate')
const writeStream = fs.createWriteStream('index3.txt')
readStream.pipe(zlib.createInflate()).pipe(writeStream)
```

### gzip 和 deflate 区别

1. 压缩算法：Gzip 使用的是 Deflate 压缩算法，该算法结合了 LZ77 算法和哈夫曼编码。LZ77 算法用于数据的重复字符串的替换和引用，而哈夫曼编码用于进一步压缩数据。
2. 压缩效率：Gzip 压缩通常具有更高的压缩率，因为它使用了哈夫曼编码来进一步压缩数据。哈夫曼编码根据字符的出现频率，将较常见的字符用较短的编码表示，从而减小数据的大小。
3. 压缩速度：相比于仅使用 Deflate 的方式，Gzip 压缩需要更多的计算和处理时间，因为它还要进行哈夫曼编码的步骤。因此，在压缩速度方面，Deflate 可能比 Gzip 更快。
4. 应用场景：Gzip 压缩常用于文件压缩、网络传输和 HTTP 响应的内容编码。它广泛应用于 Web 服务器和浏览器之间的数据传输，以减小文件大小和提高网络传输效率。

### http请求压缩

deflate 压缩前(8.2kb)   ->  压缩后(236b)

```js
const zlib = require('zlib'); 
const http = require('node:http'); 
const server = http.createServer((req,res)=>{
    const txt = '小满zs'.repeat(1000);

    //res.setHeader('Content-Encoding','gzip')
    res.setHeader('Content-Encoding','deflate')
    res.setHeader('Content-type','text/plan;charset=utf-8')
   
    const result = zlib.deflateSync(txt);
    res.end(result)
})

server.listen(3000)
```



gizp 压缩前(8.2kb)   ->  压缩后(245b)

```js
const zlib = require('zlib'); 
const http = require('node:http'); 
const server = http.createServer((req,res)=>{
    const txt = '小满zs'.repeat(1000);

    res.setHeader('Content-Encoding','gzip')
    //res.setHeader('Content-Encoding','deflate')
    res.setHeader('Content-type','text/plan;charset=utf-8')
   
    const result = zlib.gzipSync(txt);
    res.end(result)
})

server.listen(3000)
```

## http

"http" 模块是 Node.js 中用于创建和处理 HTTP 服务器和客户端的核心模块。它使得构建基于 HTTP 协议的应用程序变得更加简单和灵活。

1. 创建 Web 服务器：你可以使用 "http" 模块创建一个 HTTP 服务器，用于提供 Web 应用程序或网站。通过监听特定的端口，服务器可以接收客户端的请求，并生成响应。你可以处理不同的路由、请求方法和参数，实现自定义的业务逻辑。
2. 构建 RESTful API："http" 模块使得构建 RESTful API 变得简单。你可以使用 HTTP 请求方法（如 GET、POST、PUT、DELETE 等）和路径来定义 API 的不同端点。通过解析请求参数、验证身份和权限，以及生成相应的 JSON 或其他数据格式，你可以构建强大的 API 服务。
3. 代理服务器："http" 模块还可以用于创建代理服务器，用于转发客户端的请求到其他服务器。代理服务器可以用于负载均衡、缓存、安全过滤或跨域请求等场景。通过在代理服务器上添加逻辑，你可以对请求和响应进行修改、记录或过滤。
4. 文件服务器："http" 模块可以用于创建一个简单的文件服务器，用于提供静态文件（如 HTML、CSS、JavaScript、图像等）。通过读取文件并将其作为响应发送给客户端，你可以轻松地构建一个基本的文件服务器。

```js
const http = require('node:http'); // 引入 http 模块
const url = require('node:url'); // 引入 url 模块

// 创建 HTTP 服务器，并传入回调函数用于处理请求和生成响应
http.createServer((req, res) => {
  const { pathname, query } = url.parse(req.url, true); // 解析请求的 URL，获取路径和查询参数

  if (req.method === 'POST') { // 检查请求方法是否为 POST
    if (pathname === '/post') { // 检查路径是否为 '/post'
      let data = '';
      req.on('data', (chunk) => {
        data += chunk; // 获取 POST 请求的数据
        console.log(data);
      });
      req.on('end', () => {
        res.setHeader('Content-Type', 'application/json'); // 设置响应头的 Content-Type 为 'application/json'
        res.statusCode = 200; // 设置响应状态码为 200
        res.end(data); // 将获取到的数据作为响应体返回
      });
    } else {
      res.setHeader('Content-Type', 'application/json'); // 设置响应头的 Content-Type 为 'application/json'
      res.statusCode = 404; // 设置响应状态码为 404
      res.end('Not Found'); // 返回 'Not Found' 作为响应体
    }
  } else if (req.method === 'GET') { // 检查请求方法是否为 GET
    if (pathname === '/get') { // 检查路径是否为 '/get'
      console.log(query); // 打印查询参数中的键名为 'a' 的值
      res.end('get success'); // 返回 'get success' 作为响应体
    }else {
      res.statusCode = 404
      res.end('404')
    }
  }
}).listen(98, () => {
  console.log('server is running on port 98'); // 打印服务器启动的信息
});
```

VsCode安装REST Client

```http
POST http://localhost:98/post HTTP/1.1

Content-Type: application/json

{
    "name" : "哈哈萨拉丁了"
}

GET http://localhost:98/get?a=1&b=2 HTTP/1.1
```

## 反向代理

反向代理（Reverse Proxy）是一种网络通信模式，它充当服务器和客户端之间的中介，将客户端的请求转发到一个或多个后端服务器，并将后端服务器的响应返回给客户端。

1. 负载均衡：反向代理可以根据预先定义的算法将请求分发到多个后端服务器，以实现负载均衡。这样可以避免某个后端服务器过载，提高整体性能和可用性。
2. 高可用性：通过反向代理，可以将请求转发到多个后端服务器，以提供冗余和故障转移。如果一个后端服务器出现故障，代理服务器可以将请求转发到其他可用的服务器，从而实现高可用性。
3. 缓存和性能优化：反向代理可以缓存静态资源或经常访问的动态内容，以减轻后端服务器的负载并提高响应速度。它还可以通过压缩、合并和优化资源等技术来优化网络性能。
4. 安全性：反向代理可以作为防火墙，保护后端服务器免受恶意请求和攻击。它可以过滤恶意请求、检测和阻止攻击，并提供安全认证和访问控制。
5. 域名和路径重写：反向代理可以根据特定的规则重写请求的域名和路径，以实现 URL 路由和重定向。这对于系统架构的灵活性和可维护性非常有用。

```mermaid
graph TD
    A[客户端] -->|发送请求 /api| B{NodeJS 反向代理层}
    B -->|转发请求| C[服务端]
    C -->|返回响应| B
    B -->|返回响应| A
    
    style A fill:#e1f5fe,stroke:#01579b,stroke-width:2px
    style B fill:#f3e5f5,stroke:#4a148c,stroke-width:2px
    style C fill:#e8f5e9,stroke:#1b5e20,stroke-width:2px
```

```sh
npm install http-proxy-middleware
```

**根目录自定义配置文件**

`reverseproxy.config.js`

配置proxy代理

```js
module.exports = {
    server:{
        proxy:{
        //代理的路径
            '/api': {
                target: 'http://localhost:3000', //转发的地址
                changeOrigin: true, //是否有跨域
            }
        }
    }
}
```

index.js 实现层

```js
const http = require('node:http')
const fs = require('node:fs')
const url = require('node:url')
const html = fs.readFileSync('./index.html') //给html文件起个服务
const { createProxyMiddleware } = require('http-proxy-middleware')
const config = require('./reverseproxy.config.js')
const server = http.createServer((req, res) => {
  const { pathname } = url.parse(req.url)
  const proxyList = Object.keys(config.server.proxy) //获取代理的路径
  if (proxyList.includes(pathname)) {
    //如果请求的路径在里面匹配到 就进行代理
    const proxy = createProxyMiddleware(config.server.proxy[pathname]) //代理
    proxy(req, res)
    return
  }
  console.log(pathname, proxyList)
  res.writeHead(200, {
    'Content-Type': 'text/html',
  })
  res.end(html) //返回html
})

server.listen(96, () => {
  console.log('96服务启动')
})
```

test.js 因为我们从96端口转发到3000端口

```js
const http = require('node:http')
const url = require('node:url')


http.createServer((req, res) => {
 
    const {pathname} = url.parse(req.url)

    if(pathname === '/api'){
        res.end('success proxy')
    }
    
}).listen(3000,() =>{
    console.log('3000服务启动');
})
```

index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
          fetch('/api').then(res=>res.text()).then(res=>{
            console.log(res);
          })
    </script>
</body>
</html>
```

## 动静分离

### 什么是动静分离？

动静分离是一种在Web服务器架构中常用的优化技术，旨在提高网站的性能和可伸缩性。它基于一个简单的原则：将动态生成的内容（如动态网页、API请求）与静态资源（如HTML、CSS、JavaScript、图像文件）分开处理和分发。

通过将动态内容和静态资源存储在不同的服务器或服务上，并使用不同的处理机制，可以提高网站的处理效率和响应速度。这种分离的好处包括：

1. **性能优化**：将静态资源与动态内容分离可以提高网站的加载速度。由于静态资源往往是不变的，可以使用缓存机制将其存储在CDN（内容分发网络）或浏览器缓存中，从而减少网络请求和数据传输的开销。
2. **负载均衡**：通过将动态请求分发到不同的服务器或服务上，可以平衡服务器的负载，提高整个系统的可伸缩性和容错性。
3. **安全性**：将动态请求与静态资源分开处理可以提高系统的安全性。静态资源通常是公开可访问的，而动态请求可能涉及敏感数据或需要特定的身份验证和授权。通过将静态资源与动态内容分离，可以更好地管理访问控制和安全策略。

实现动静分离的方法

- 使用反向代理服务器（如Nginx、Apache）将静态请求和动态请求转发到不同的后端服务器或服务。
- 将静态资源部署到CDN上，通过CDN分发静态资源，减轻源服务器的负载。
- 使用专门的静态文件服务器（如Amazon S3、Google Cloud Storage）存储和提供静态资源，而将动态请求交给应用服务器处理。

```js
import http from 'node:http' // 导入http模块
import fs from 'node:fs' // 导入文件系统模块
import path from 'node:path' // 导入路径处理模块
import mime from 'mime' // 导入mime模块

const server = http.createServer((req, res) => {
  const { method, url } = req
  if (method === 'GET' && url.startsWith('/static')) {
    const filePath = path.join(process.cwd(), url) // 获取文件路径
    const mimeType = mime.getType(filePath) // 获取文件的MIME类型
    console.log(mimeType) // 打印MIME类型

    fs.readFile(filePath, (err, data) => {
      // 读取文件内容
      if (err) {
        res.writeHead(404, {
          'Content-Type': 'text/plain', // 设置响应头为纯文本类型
        })
        res.end('not found') // 返回404 Not Found
      } else {
        res.writeHead(200, {
          'Content-Type': mimeType, // 设置响应头为对应的MIME类型
          'Cache-Control': 'public, max-age=3600', // 设置缓存控制头
        })
        res.end(data) // 返回文件内容
      }
    })
  }

  // 处理动态资源
  if ((method === 'GET' || method === 'POST') && url.startsWith('/api')) {
    // ...处理动态资源的逻辑
  }
})
server.listen(80, () => {
  console.log('server runing at http://127.0.0.1')
})
```

## 邮件服务

需要用到库

```sh
npm install js-yaml
npm install nodemailer
```

我们邮件的账号（密码| 授权码）不可能明文写到代码里面一般存放在yaml文件或者环境变量里面

> js-yaml 解析yaml文件

```yaml
pass: 授权码 | 密码
user: xxxxx@qq.com 邮箱账号
```

```js
import nodemailder from 'nodemailer'
import yaml from 'js-yaml'
import fs from 'node:fs'
import http from 'node:http'
import url from 'node:url'

const mailInfo = yaml.load(fs.readFileSync('./mail.yaml', 'utf8'))

//初始化邮件服务
const transPort = nodemailder.createTransport({
  service: 'qq', //服务商
  host: 'smtp.qq.com',
  port: 465,
  secure: true,
  auth: {
    pass: mailInfo.pass, //密码 | 授权码
    user: mailInfo.user, //邮箱
  },
})

http
  .createServer((req, res) => {
    const { pathname } = url.parse(req.url)
    const { method } = req
    if (method === 'POST' && pathname == '/send/mail') {
      // 发送邮件
      let data = ''
      req.on('data', (chunk) => {
        data += chunk
      })
      req.on('end', () => {
        const { to, subject, text } = JSON.parse(data)
        transPort.sendMail({
          to,
          from: mailInfo.user,
          subject,
          text,
        })
        res.end('ok')
      })
    }
  })
  .listen(3000, () => {
    console.log('listening on port 3000')
  })
```

> mail.http

```http
POST http://localhost:3000/send/mail HTTP/1.1
Content-Type: application/json

{
    "to":"123@qq.com",
    "subject":"测试邮件",
    "text":"1235456阿三打什么"
}
```

## express

### 什么是express？

Express是一个流行的Node.js Web应用程序框架，用于构建灵活且可扩展的Web应用程序和API。它是基于Node.js的HTTP模块而创建的，简化了处理HTTP请求、响应和中间件的过程。

1. 简洁而灵活：Express提供了简单而直观的API，使得构建Web应用程序变得简单快捷。它提供了一组灵活的路由和中间件机制，使开发人员可以根据需求定制和组织应用程序的行为。
2. 路由和中间件：Express使用路由和中间件来处理HTTP请求和响应。开发人员可以定义路由规则，将特定的URL路径映射到相应的处理函数。同时，中间件允许开发人员在请求到达路由处理函数之前或之后执行逻辑，例如身份验证、日志记录和错误处理。
3. 路由模块化：Express支持将路由模块化，使得应用程序可以根据不同的功能或模块进行分组。这样可以提高代码的组织性和可维护性，使得多人协作开发更加便捷。
4. 视图引擎支持：Express可以与各种模板引擎集成，例如EJS、Pug（以前称为Jade）、Handlebars等。这使得开发人员可以方便地生成动态的HTML页面，并将数据动态渲染到模板中。
5. 中间件生态系统：Express有一个庞大的中间件生态系统，开发人员可以使用各种中间件来扩展和增强应用程序的功能，例如身份验证、会话管理、日志记录、静态文件服务等。

### 编码

- 启动一个http服务

```js
import express from 'express';

const app = express() //express 是个函数

app.listen(3000, () => console.log('Listening on port 3000'))
```

- 编写get post 接口

```js
app.get('/', (req, res) => {
    res.send('get')
})

app.post('/create', (req, res) => {
    res.send('post')
})
```

- 接受前端的参数

```js
app.use(express.json()) //如果前端使用的是post并且传递json 需要注册此中间件 不然是undefined

app.get('/', (req, res) => {
    console.log(req.query) //get 用query
    res.send('get')
})

app.post('/create', (req, res) => {
    console.log(req.body) //post用body
    res.send('post')
})

//如果是动态参数用 params
app.get('/:id', (req, res) => {
    console.log(req.params)
    res.send('get id')
})
```

### 模块化

> 我们正常开发的时候肯定不会把代码写到一个模块里面，Express允许将路由处理程序拆分为多个模块，每个模块负责处理特定的路由。通过将路由处理程序拆分为模块，可以使代码逻辑更清晰，易于维护和扩展

```txt
src
 --user.js
 --list.js
app.js
```

src/user.js

```js
import express from 'express'

const router = express.Router() //路由模块


router.post('/login', (req, res) => {
    res.send('login')
})

router.post('/register', (req, res) => {
    res.send('register')
})


export default router
```

app.js

```js
import express from 'express';
import User from './src/user.js'
const app = express()
app.use(express.json())
app.use('/user', User)
app.get('/', (req, res) => {
    console.log(req.query)
    res.send('get')
})

app.get('/:id', (req, res) => {
    console.log(req.params)
    res.send('get id')
})

app.post('/create', (req, res) => {
    console.log(req.body)
    res.send('post')
})


app.listen(3000, () => console.log('Listening on port 3000'))
```

### 中间件

中间件是一个关键概念。中间件是处理HTTP请求和响应的函数，它位于请求和最终路由处理函数之间，可以对请求和响应进行修改、执行额外的逻辑或者执行其他任务。

中间件函数接收三个参数：`req`（请求对象）、`res`（响应对象）和`next`（下一个中间件函数）。通过调用`next()`方法，中间件可以将控制权传递给下一个中间件函数。如果中间件不调用`next()`方法，请求将被中止，不会继续传递给下一个中间件或路由处理函数

- 实现一个日志中间件

```sh
npm install log4js
```

log4js是一个用于Node.js应用程序的流行的日志记录库，它提供了灵活且可配置的日志记录功能。log4js允许你在应用程序中记录不同级别的日志消息，并可以将日志消息输出到多个目标，如控制台、文件、数据库等

express\middleware\logger.js

```js
import log4js from 'log4js';

// 配置 log4js
log4js.configure({
  appenders: {
    out: {
      type: 'stdout', // 输出到控制台
      layout: {
        type: 'colored' // 使用带颜色的布局
      }
    },
    file: {
      type: 'file', // 输出到文件
      filename: './logs/server.log', // 指定日志文件路径和名称
    }
  },
  categories: {
    default: {
      appenders: ['out', 'file'], // 使用 out 和 file 输出器
      level: 'debug' // 设置日志级别为 debug
    }
  }
});

// 获取 logger
const logger = log4js.getLogger('default');

// 日志中间件
const loggerMiddleware = (req, res, next) => {
  logger.debug(`${req.method} ${req.url}`); // 记录请求方法和URL
  next();
};

export default loggerMiddleware;
```

app.js

```js
import express from 'express';
import User from './src/user.js'
import loggerMiddleware from './middleware/logger.js';
const app = express()
app.use(loggerMiddleware)
```

## 防盗链

1. 通过HTTP引用检查：网站可以检查HTTP请求的来源，如果来源网址与合法的来源不匹配，就拒绝提供资源。这可以通过服务器配置文件或特定的脚本实现。
2. 使用Referrer检查：网站可以检查HTTP请求中的Referrer字段，该字段指示了请求资源的来源页面。如果Referrer字段不符合预期，就拒绝提供资源。这种方法可以在服务器配置文件或脚本中实现。
3. 使用访问控制列表（ACL）：网站管理员可以配置服务器的访问控制列表，只允许特定的域名或IP地址访问资源，其他来源的请求将被拒绝。
4. 使用防盗链插件或脚本：一些网站平台和内容管理系统提供了专门的插件或脚本来防止盗链。这些工具可以根据需要配置，阻止来自未经授权的网站的盗链请求。
5. 使用水印技术：在图片或视频上添加水印可以帮助识别盗链行为，并提醒用户资源的来源。

**编码**

- 第一步需要初始化静态资源目录 `express.static`

```js
import express from 'express'

const app = express()
        //自定义前缀   初始化目录
app.use('/assets',express.static('static'))


app.listen(3000,()=>{
    console.log('listening on port 3000')
})
```

增加防盗链

防盗链一般主要就是验证 `host`  或者  `referer` 

```js
import express from 'express';

const app = express();

const whitelist = ['localhost']; //配置网址 IP

// 防止热链中间件
const preventHotLinking = (req, res, next) => {
  const referer = req.get('referer'); // 获取请求头部中的 referer 字段
  if (referer) {
    const { hostname } = new URL(referer); // 从 referer 中解析主机名
    if (!whitelist.includes(hostname)) { // 检查主机名是否在白名单中
      res.status(403).send('Forbidden'); // 如果不在白名单中，返回 403 Forbidden
      return;
    }
  }
  next(); // 如果在白名单中，继续处理下一个中间件或路由
};

app.use(preventHotLinking); // 应用防止热链中间件
app.use('/assets', express.static('static')); // 处理静态资源请求

app.listen(3000, () => {
  console.log('Listening on port 3000'); // 启动服务器，监听端口3000
});
```

## 响应头和请求头

### 响应头

HTTP响应头（HTTP response headers）是在HTTP响应中发送的元数据信息，用于描述响应的特性、内容和行为。它们以键值对的形式出现，每个键值对由一个标头字段（header field）和一个相应的值组成。

例如以下示例

```http
Access-Control-Allow-Origin:*
Cache-Control:public, max-age=0, must-revalidate
Content-Type:text/html; charset=utf-8
Server:nginx
Date:Mon, 08 Jan 2024 18:32:47 GMT
```

### 响应头和跨域之间的关系

- cors

跨域资源共享（Cross-Origin Resource Sharing，CORS）是一种机制，用于在浏览器中实现跨域请求访问资源的权限控制。当一个网页通过 XMLHttpRequest 或 Fetch API 发起跨域请求时，浏览器会根据同源策略（Same-Origin Policy）进行限制。`同源策略要求请求的源（协议、域名和端口）必须与资源的源相同，否则请求会被浏览器拒绝`

- 发送请求

```js
fetch('http://localhost:3000/info').then(res=>{
    return res.json()
}).then(res=>{
    console.log(res)
})
```

- express 编写一个get接口

```js
import express from 'express'
const app = express()
app.get('/info', (req, res) => {
    res.json({
        code: 200
    })
})
app.listen(3000, () => {
    console.log('http://localhost:3000')
}
```

发现是有报错的 根据同源策略我们看到`协议一样，域名一样，但是端口不一致`，端口也无法一致，会有冲突，否则就是前后端不分离的项目，前后端代码放在一起，只用一个端口，不过我们是分离的没法这么做。

```sh
npm install nodemon
```

这时候我们就需要后端支持一下，跨域请求资源放行

```js
Access-Control-Allow-Origin: * | Origin
```

增加以下 `响应头` 允许localhost 5500 访问

```js
app.use('*',(req,res,next)=>{
     //*  允许所有资源访问
    res.setHeader('Access-Control-Allow-Origin','http://localhost:5500') //允许localhost 5500 访问
    next()
})
```

结果返回  { code:200 }

### 请求头

默认情况下cors仅支持客户端向服务器发送如下九个请求头

> tips 没有application/json

1. Accept：指定客户端能够处理的内容类型。
2. Accept-Language：指定客户端偏好的自然语言。
3. Content-Language：指定请求或响应实体的自然语言。
4. Content-Type：指定请求或响应实体的媒体类型。
5. DNT (Do Not Track)：指示客户端不希望被跟踪。
6. Origin：指示请求的源（协议、域名和端口）。
7. User-Agent：包含发起请求的用户代理的信息。
8. Referer：指示当前请求的源 URL。
9. Content-type: application/x-www-form-urlencoded | multipart/form-data |  text/plain

如果客户端需要支持额外的请求那么我们需要在客户端支持

```js
'Access-Control-Allow-Headers','Content-Type' //支持application/json
```

### 请求方法支持

**我们服务端默认只支持 GET POST HEAD OPTIONS 请求**

例如我们遵循restFui 要支持`PATCH` 或者其他请求

增加patch

```js
app.patch('/info', (req, res) => {
    res.json({
        code: 200
    })
})
```

发送patch

```js
fetch('http://localhost:3000/info',{
            method:'PATCH',
}).then(res=>{
    return res.json()
}).then(res=>{
    console.log(res)
})
```

发现报错说patch不在我们的methods里面

修改如下

```js
'Access-Control-Allow-Methods','POST,GET,OPTIONS,DELETE,PATCH'
```

结果返回  { code:200 }

### 预检请求 OPTIONS

预检请求的主要目的是确保跨域请求的安全性 它需要满足一定条件才会触发

1. 自定义请求方法：当使用非简单请求方法（Simple Request Methods）时，例如 PUT、DELETE、CONNECT、OPTIONS、TRACE、PATCH 等，浏览器会发送预检请求。
2. 自定义请求头部字段：当请求包含自定义的头部字段时，浏览器会发送预检请求。自定义头部字段是指不属于简单请求头部字段列表的字段，例如 Content-Type 为 application/json、Authorization 等。
3. 带凭证的请求：当请求需要在跨域环境下发送和接收凭证（例如包含 cookies、HTTP 认证等凭证信息）时，浏览器会发送预检请求。

- 尝试发送预检请求

```js
 fetch('http://localhost:3000/info',{
    method:'POST',
    headers:{
        'Content-Type':'application/json'
    },
    body:JSON.stringify({name:'xmzs'})
}).then(res=>{
    return res.json()
}).then(res=>{
    console.log(res)
})
```

- express

```js
app.post('/info', (req, res) => {
    res.json({
        code: 200
    })
})
```

发现报错了

因为 `application/json` 不属于cors 范畴需要手动支持

```js
'Access-Control-Allow-Headers','Content-Type'
```

结果返回  { code:200 }

### 自定义响应头

在我们做需求的时候肯定会碰到后端自定义响应头

```js
app.get('/info', (req, res) => {
    res.set('xmzs', '1')
    res.json({
        code: 200
    })
})
```

前端如何读取呢？

```js
fetch('http://localhost:3000/info').then(res=>{
    const headers = res.headers 
    console.log(headers.get('xmzs')) //读取自定义响应头
    return res.json()
}).then(res=>{
    console.log(res)
})
```

发现是null 这是因为后端没有抛出该响应头所以后端需要增加抛出的一个字段

```js
app.get('/info', (req, res) => {
    res.set('xmzs', '1')
    res.setHeader('Access-Control-Expose-Headers', 'xmzs')
    res.json({
        code: 200
    })
})
```

### SSE技术

Server-Sent Events（SSE）是一种在客户端和服务器之间实现单向事件流的机制，允许服务器主动向客户端发送事件数据。在 SSE 中，可以使用自定义事件（Custom Events）来发送具有特定类型的事件数据。

```
webSocket属于全双工通讯，也就是前端可以给后端实时发送，后端也可以给前端实时发送，SSE属于单工通讯，后端可以给前端实时发送
```

- express 增加该响应头`text/event-stream`就变成了sse event 事件名称 data 发送的数据

```js
app.get('/sse',(req,res)=>{
    res.setHeader('Content-Type', 'text/event-stream')
    res.status(200)
    setInterval(() => {
        res.write('event: test\n')
        res.write('data: ' + new Date().getTime() + '\n\n')
    }, 1000)
})
```

前端接受

```js
const sse = new EventSource('http://localhost:3000/sse')
sse.addEventListener('test', (event) => {
    console.log(event.data)
})
```

## mysql2

### 安装依赖

```sh
npm install mysql2 express js-yaml
```

1. mysql2 用来连接mysql和编写sq语句
2. express 用来提供接口 增删改差
3. js-yaml 用来编写配置文件

### 编写代码

db.config.yaml

```yaml
db:
   host: localhost #主机
   port: 3306 #端口
   user: root #账号
   password: '1234' #密码 一定要字符串
   database: test # 库
```

index.js

```js
import mysql2 from 'mysql2/promise'
import fs from 'node:fs'
import jsyaml from 'js-yaml'
import express from 'express'

const yaml = fs.readFileSync('./db.config.yaml', 'utf8')
const config = jsyaml.load(yaml)
const sql = await mysql2.createConnection({
  ...config.db,
})
const app = express()

app.use(express.json())

//查询接口 全部
app.get('/', async (req, res) => {
  const [data] = await sql.query('select * from user')
  res.send(data)
})

//单个查询 params
app.get('/user/:id', async (req, res) => {
  const [row] = await sql.query(`select * from user where id = ?`, [req.params.id])
  res.send(row)
})

//新增接口
app.post('/create', async (req, res) => {
  const { name, age, address } = req.body
  await sql.query(`insert into user(name,age,address,create_time) values(?,?,?,NOW())`, [
    name,
    age,
    address
  ])
  res.send({ ok: 1 })
})

//编辑
app.post('/update', async (req, res) => {
  const { name, age, address, id } = req.body
  await sql.query(`update user set name = ?,age = ?,address = ? where id = ?`, [name, age, address, id])
  res.send({ ok: 1 })
})

//删除
app.post('/delete', async (req, res) => {
  await sql.query(`delete from user where id = ?`, [req.body.id])
  res.send({ ok: 1 })
})
const port = 3000

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`)
})
```

index.http

方便测试接口

```http
# 查询全部
 GET http://localhost:3000/ HTTP/1.1

# 单个查询
GET http://localhost:3000/user/2 HTTP/1.1

# 添加数据
POST http://localhost:3000/create HTTP/1.1
Content-Type: application/json

{
    "name":"张三",
    "age":18,
    "address":"北京"
}

# 更新数据
POST http://localhost:3000/update HTTP/1.1
Content-Type: application/json

{
    "name":"法外狂徒",
    "age":20,
    "id":11
}


#删除
# POST http://localhost:3000/delete HTTP/1.1
# Content-Type: application/json

# {
#     "id":11
# }
```

## knex

Knex是一个基于JavaScript的`查询生成器`，它允许你使用JavaScript代码来生成和执行SQL查询语句。它提供了一种简单和直观的方式来与关系型数据库进行交互，而无需直接编写SQL语句。你可以使用Knex定义表结构、执行查询、插入、更新和删除数据等操作。

### Knex的安装和设置

> knex支持多种数据库 pg sqlite3 mysql2 oracledb tedious

用什么数据库安装对应的数据库就行了

```sh
#安装knex
$ npm install knex --save

#安装你用的数据库
$ npm install pg
$ npm install pg-native
$ npm install sqlite3
$ npm install better-sqlite3
$ npm install mysql
$ npm install mysql2
$ npm install oracledb
$ npm install tedious
```

连接数据库

```js
import knex from 'knex'
const db = knex({
    client: "mysql2",
    connection: config.db
})
```

```yaml
db:
   host: localhost #主机
   port: 3306 #端口
   user: root #账号
   password: '1234' #密码 一定要字符串
   database: test # 库
```

### 定义表结构

```js
db.schema.createTableIfNotExists('list', table => {
  table.increments('id') //id自增
  table.integer('age') //age 整数
  table.string('name') //name 字符串
  table.string('hobby') //hobby 字符串
  table.timestamps(true, true) //创建时间和更新时间
}).then(() => {
    console.log('创建成功')
})
```

### 实现增删改查

```js
import mysql2 from 'mysql2/promise'
import fs from 'node:fs'
import jsyaml from 'js-yaml'
import express from 'express'
import knex from 'knex'
const yaml = fs.readFileSync('./db.config.yaml', 'utf8')
const config = jsyaml.load(yaml)
// const sql = await mysql2.createConnection({
//    ...config.db
// })
const db = knex({
    client: "mysql2",
    connection: config.db
})

const app = express()
app.use(express.json())
//查询接口 全部
app.get('/', async (req, res) => {
    const data = await db('list').select().orderBy('id', 'desc')
    const total = await db('list').count('* as total')
    res.json({
        code: 200,
        data,
        total: total[0].total,
    })
})
//单个查询 params
app.get('/user/:id', async (req, res) => {
    const row = await db('list').select().where({ id: req.params.id })
    res.json({
        code: 200,
        data: row
    })
})

//新增接口
app.post('/create', async (req, res) => {
    const { name, age, hobby } = req.body
    const detail = await db('list').insert({ name, age, hobby })
    res.send({
        code: 200,
        data: detail
    })
})

//编辑
app.post('/update', async (req, res) => {
    const { name, age, hobby, id } = req.body
    const info = await db('list').update({ name, age, hobby }).where({ id })
    res.json({
        code: 200,
        data: info
    })
})
//删除
app.post('/delete', async (req, res) => {
    const info = await db('list').delete().where({ id: req.body.id })
    res.json({
        code: 200,
        data: info
    })
})
const port = 3000

app.listen(port, () => {
    console.log(`Example app listening on port ${port}`)
})
```

### 事务

你可以使用事务来确保一组数据库操作的原子性，即要么全部成功提交，要么全部回滚

例如A给B转钱，需要两条语句，如果A语句成功了，B语句因为一些场景失败了，那这钱就丢了，所以事务就是为了解决这个问题，要么都成功，要么都回滚，保证金钱不会丢失。

```js
//伪代码
db.transaction(async (trx) => {
    try {
        await trx('list').update({money: -100}).where({ id: 1 }) //A
        await trx('list').update({money: +100}).where({ id: 2 }) //B
        await trx.commit() //提交事务
    }
    catch (err) {
        await trx.rollback() //回滚事务
    }
}).then(()=>{
    console.log('成功')
}).catch(()=>{
    console.log('失败')
})
```

## prisma

Prisma 是一个现代化的数据库工具套件，用于简化和改进应用程序与数据库之间的交互。它提供了一个类型安全的查询构建器和一个强大的 ORM（对象关系映射）层，使开发人员能够以声明性的方式操作数据库。

Prisma 支持多种主流数据库，包括 PostgreSQL、MySQL 和 SQLite，它通过生成标准的数据库模型来与这些数据库进行交互。使用 Prisma，开发人员可以定义数据库模型并生成类型安全的查询构建器，这些构建器提供了一套直观的方法来创建、更新、删除和查询数据库中的数据。

Prisma 的主要特点包括：

1. 类型安全的查询构建器：Prisma 使用强类型语言（如 TypeScript）生成查询构建器，从而提供了在编译时捕获错误和类型检查的能力。这有助于减少错误，并提供更好的开发人员体验。
2. 强大的 ORM 层：Prisma 提供了一个功能强大的 ORM 层，使开发人员能够以面向对象的方式操作数据库。它自动生成了数据库模型的 CRUD（创建、读取、更新、删除）方法，简化了与数据库的交互。
3. 数据库迁移：Prisma 提供了数据库迁移工具，可帮助开发人员管理数据库模式的变更。它可以自动创建和应用迁移脚本，使数据库的演进过程更加简单和可控。
4. 性能优化：Prisma 使用先进的查询引擎和数据加载技术，以提高数据库访问的性能。它支持高级查询功能，如关联查询和聚合查询，并自动优化查询以提供最佳的性能

文件路径只需这样

```Text
文件名
├── .env
└── prisma/
```

### 安装使用

安装 Prisma CLI：

- 使用 npm 安装：运行 `npm install -g prisma`。
- 使用 yarn 安装：运行 `yarn global add prisma`。
- 查看命令  `prisma init -h`

初始化项目

- 使用`prisma init --datasource-provider mysql`

连接mysql

- 修改.env文件 `[DATABASE_URL="mysql://账号:密码@主机:端口/库名"]`
- 例子 `DATABASE_URL="mysql://root:123456@localhost:3306/xiaoman"`

#### 创建表

在prisma/schema.prisma文件下写入下面

```js

generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "mysql"
  url      = env("DATABASE_URL")
}

//编写表结构

// 文章表
model Post {
  id       Int     @id @default(autoincrement()) //id 整数 自增
  title    String //title字符串类型
  publish  Boolean @default(false) //发布 布尔值默认false
  author   User    @relation(fields: [authorId], references: [id]) //作者 关联用户表 关联关系 authorId 关联user表的id
  authorId Int
}

model User {
  id    Int    @id @default(autoincrement())
  name  String
  email String @unique
  posts Post[]
}
```

执行命令 创建表

> 用此命令一定要注意是否覆盖当前库里面的所有内容，建议使用新库去做测试

```sh
prisma migrate dev
```

### 实现增删改查

```sh
npm i express

npm i --save-dev @types/express

npm install --save-dev tsx
```



```ts
import express from 'express'
import { PrismaClient } from '@prisma/client'
const prisma = new PrismaClient()
const app = express()
const port: number = 3000


app.use(express.json())

//关联查找
app.get('/', async (req, res) => {
    const data = await prisma.user.findMany({
        include: {
            posts: true
        }
    })
    res.send(data)
})
//单个查找
app.get('/user/:id', async (req, res) => {
   const row =  await prisma.user.findMany({
        where: {
            id: Number(req.params.id)
        }
    })
    res.send(row)
})
//新增
app.post('/create', async (req, res) => {
    const { name, email } = req.body
    const data = await prisma.user.create({
        data: {
            name,
            email,
            posts: {
                create: {
                    title: '标题',
                    publish: true
                },
            }
        }
    })
    res.send(data)
})

//更新
app.post('/update', async (req, res) => {
    const { id, name, email } = req.body
    const data = await prisma.user.update({
        where: {
            id: Number(id)
        },
        data: {
            name,
            email
        }
    })
    res.send(data)
})

//删除
app.post('/delete', async (req, res) => {
    const { id } = req.body
    await prisma.post.deleteMany({
        where: {
            authorId: Number(id)
        }
    })
    const data = await prisma.user.delete({
        where: {
            id: Number(id),
        },
    })
    res.send(data)
})


app.listen(port, () => {
    console.log(`App listening on port ${port}`)
})
```

