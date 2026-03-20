## 学习TypeScript

### 认识基础类型

下载组件库

```sh
npm install typescript -g
```

创建一个ts文件并且初始化`tsc --init` ,在执行`tsc -w`

创建文件：

1.tsc file’s name -w :监听ts文件生成为js文件

2.node file's name 编译js文件

类型：

1.基础类型：Boolean、Number、underfine、null、String、Symbol、BigInt

严格模式配置文件（tsconfig)；

```typescript
{
    "compilerOptions":{
      "strict": true //严格模式的开启和关闭
    }
}
```

### 任意类型

安装组件库

```sh
npm i @types/node --save-dev
npm i ts-node --g
// 安装tsx可以直接运行
npm install -g tsx
tsx file.ts
```

1、any 任意类型 unknown 不知道类型 ->属于顶级类型

2、Object

3、Number String Boolean

4、Number String Boolean

5、1........... '小白' .........true

6、never

### 接口和对象类型

```typescript
// interface 重名 重合
// interface 任意key [propName:string]:any索引签名
// interface ? 可选 readonly 只读
// interface 接口继承 extends
// interface 定义函数类型
//不能多属性 也不能少属性


interface Axx extends Bx {
    readonly id: number
    name: string
    age?: number
    readonly cb: () => boolean
}

interface Bx {
    xxx: string
}

let a: Axx = {
    id: 1,
    name: "小白",
    age: 88,
    xxx: 'xxx',
    cb: () => {
        return false
    }
}
console.log(a)

interface Fn {
    (name:string):number[]
}

const fn:Fn = function (name:string) {
    return [1]
}
```

### 数组类型

```typescript
//number[]
//Array<boolean>
//定义数组
interface X {
    name: string
    age?: number
}
let arr: X[] = [{ name: '小白' }, { name: '小青', age: 12 }]
// 定义对象数组使用interface
```

```ts
//二维数组
// let arr: number[][] = [[1, 2], [3, 4]]
// Array<Array<number>>
// any[]
// 大小不确定的数组
// let arr: any[] = [1, '2', true, {}, []]
let arr: number[][] = [[], []]

console.log(arr)
```

```typescript
function a(...args: string[]) {
    console.log(args)
}

a('1', '2', '3', '4')
```

### 函数类型

函数定义类型和返回值|箭头函数定义类型和返回值

```typescript
function add(a: number, b: number): number {
    return a + b;
}

const subtract = (a: number, b: number): number => {
    return a - b;
}
console.log(add(2, 3)); // Output: 5
console.log(subtract(5, 2)); // Output: 3
```

函数默认的参数|函数可选参数

```typescript
function add(a: number = 10, b: number): number {
    return a + b;
}
//可选
function add(a: number, b?: number): number {
    return a + b; //NaN
}
```

参数是一个对象如何定义

```typescript
interface Person {
  name: string;
  age: number;
}

function greet(person: Person): string {
  return `Hello, ${person.name}! You are ${person.age} years old.`;
}

console.log(greet({ name: "Alice", age: 30 }));
```

函数this类型，函数重载

```typescript
interface Obj {
    user: number[],
    add: (this: Obj, num: number) => void
}
// ts 可以定义this的类型 在js中无法使用 必须是第一个参数定义this的类型
let obj:Obj = {
    user:[1,2,3],
    add(this:Obj,num:number) {
        this.user.push(num)
    }
}

obj.add(4)
console.log(obj)
```

```typescript
// 函数重载
let user: number[] = [1, 2, 3]
function findNum(add: number[]): number[] //如果传入一个number类型的数组 就把这个数组添加到user中
function findNum(id: number): number[] //如果传递了id就是单个查询
function findNum(): number[]  //如果没有传入东西就是查询所有
function findNum(ids?: number | number[]): number[] {
    if (typeof ids === 'number') {
        return user.filter(item => item === ids)
    }
    else if (Array.isArray(ids)) {
        user.push(...ids)
        return user
    } else {
        return user
    }
}

console.log(findNum()) //查询所有
console.log(findNum(2)) //查询单个
console.log(findNum([4, 5])) //添加数组
```

### 类型断言 | 联合类型 | 交叉类型
