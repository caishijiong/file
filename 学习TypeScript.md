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

```typescript
//联合类型
let phone:number | string = 3123709
let phone:number | string = '090-123535'
console.log(phone)

let fn = function(type:number|boolean):boolean {
    return !!type
}

let result = fn(1)
console.log(result)
```

```typescript
// 交叉类型
interface Pople {
    name: string
    age: number
}

interface Man {
    sex: number
}
const xiaobai = (man: Pople & Man): void => {
    console.log(man);
}
xiaobai({
    name: '小白',
    age: 10,
    sex: 1
})
```

```typescript
// 类型断言-只能欺骗编译器但是不能防止报错-不能滥用
let fn = function(num:number | string):void {
    console.log((num as string).length)
}

fn(2138)
```

### 内置对象

**ECMAScript的内置对象有: Boolean、Number、String、RegExp、Date、Error**

```typescript
let b: Boolean = new Boolean(1)
console.log(b)
let n: Number = new Number(true)
console.log(n)
let s: String = new String('哔哩哔哩关注小满zs')
console.log(s)
let d: Date = new Date()
console.log(d)
let r: RegExp = /^1/
console.log(r)
let e: Error = new Error("error!")
console.log(e)
```

**DOM和BOM的内置对象有: **`Document`、`HTMLElement`、`Event`、`NodeList`  **等**

```typescript
let body: HTMLElement = document.body;
let allDiv: NodeList = document.querySelectorAll('div');
//读取div 这种需要类型断言 或者加个判断应为读不到返回null
let div:HTMLElement = document.querySelector('div') as HTMLDivElement
document.addEventListener('click', function (e: MouseEvent) {
    
});
//dom元素的映射表
interface HTMLElementTagNameMap {
    "a": HTMLAnchorElement;
    "abbr": HTMLElement;
    "address": HTMLElement;
    "applet": HTMLAppletElement;
    "area": HTMLAreaElement;
    "article": HTMLElement;
    "aside": HTMLElement;
    "audio": HTMLAudioElement;
    "b": HTMLElement;
    "base": HTMLBaseElement;
    "bdi": HTMLElement;
    "bdo": HTMLElement;
    "blockquote": HTMLQuoteElement;
    "body": HTMLBodyElement;
    "br": HTMLBRElement;
    "button": HTMLButtonElement;
    "canvas": HTMLCanvasElement;
    "caption": HTMLTableCaptionElement;
    "cite": HTMLElement;
    "code": HTMLElement;
    "col": HTMLTableColElement;
    "colgroup": HTMLTableColElement;
    "data": HTMLDataElement;
    "datalist": HTMLDataListElement;
    "dd": HTMLElement;
    "del": HTMLModElement;
    "details": HTMLDetailsElement;
    "dfn": HTMLElement;
    "dialog": HTMLDialogElement;
    "dir": HTMLDirectoryElement;
    "div": HTMLDivElement;
    "dl": HTMLDListElement;
    "dt": HTMLElement;
    "em": HTMLElement;
    "embed": HTMLEmbedElement;
    "fieldset": HTMLFieldSetElement;
    "figcaption": HTMLElement;
    "figure": HTMLElement;
    "font": HTMLFontElement;
    "footer": HTMLElement;
    "form": HTMLFormElement;
    "frame": HTMLFrameElement;
    "frameset": HTMLFrameSetElement;
    "h1": HTMLHeadingElement;
    "h2": HTMLHeadingElement;
    "h3": HTMLHeadingElement;
    "h4": HTMLHeadingElement;
    "h5": HTMLHeadingElement;
    "h6": HTMLHeadingElement;
    "head": HTMLHeadElement;
    "header": HTMLElement;
    "hgroup": HTMLElement;
    "hr": HTMLHRElement;
    "html": HTMLHtmlElement;
    "i": HTMLElement;
    "iframe": HTMLIFrameElement;
    "img": HTMLImageElement;
    "input": HTMLInputElement;
    "ins": HTMLModElement;
    "kbd": HTMLElement;
    "label": HTMLLabelElement;
    "legend": HTMLLegendElement;
    "li": HTMLLIElement;
    "link": HTMLLinkElement;
    "main": HTMLElement;
    "map": HTMLMapElement;
    "mark": HTMLElement;
    "marquee": HTMLMarqueeElement;
    "menu": HTMLMenuElement;
    "meta": HTMLMetaElement;
    "meter": HTMLMeterElement;
    "nav": HTMLElement;
    "noscript": HTMLElement;
    "object": HTMLObjectElement;
    "ol": HTMLOListElement;
    "optgroup": HTMLOptGroupElement;
    "option": HTMLOptionElement;
    "output": HTMLOutputElement;
    "p": HTMLParagraphElement;
    "param": HTMLParamElement;
    "picture": HTMLPictureElement;
    "pre": HTMLPreElement;
    "progress": HTMLProgressElement;
    "q": HTMLQuoteElement;
    "rp": HTMLElement;
    "rt": HTMLElement;
    "ruby": HTMLElement;
    "s": HTMLElement;
    "samp": HTMLElement;
    "script": HTMLScriptElement;
    "section": HTMLElement;
    "select": HTMLSelectElement;
    "slot": HTMLSlotElement;
    "small": HTMLElement;
    "source": HTMLSourceElement;
    "span": HTMLSpanElement;
    "strong": HTMLElement;
    "style": HTMLStyleElement;
    "sub": HTMLElement;
    "summary": HTMLElement;
    "sup": HTMLElement;
    "table": HTMLTableElement;
    "tbody": HTMLTableSectionElement;
    "td": HTMLTableDataCellElement;
    "template": HTMLTemplateElement;
    "textarea": HTMLTextAreaElement;
    "tfoot": HTMLTableSectionElement;
    "th": HTMLTableHeaderCellElement;
    "thead": HTMLTableSectionElement;
    "time": HTMLTimeElement;
    "title": HTMLTitleElement;
    "tr": HTMLTableRowElement;
    "track": HTMLTrackElement;
    "u": HTMLElement;
    "ul": HTMLUListElement;
    "var": HTMLElement;
    "video": HTMLVideoElement;
    "wbr": HTMLElement;
}
```

**定义Promise 如果我们不知道返回的类型TS是推断不出来返回的是什么类型**

```typescript
function promise():Promise<number>{
   return new Promise<number>((resolve,reject)=>{
       resolve(1)
   })
}
 
promise().then(res=>{
    console.log(res)
})
```

代码雨

```typescript
let canvas = document.querySelector('#canvas') as HTMLCanvasElement
let ctx = canvas.getContext('2d') as CanvasRenderingContext2D
canvas.height = screen.availHeight; //可视区域的高度
canvas.width = screen.availWidth; //可视区域的宽度
let str: string[] = 'asmdamsdma'.split('') // 随意字母
let Arr = Array(Math.ceil(canvas.width / 10)).fill(0) //获取宽度例如1920 / 10 192
console.log(Arr);
 
const rain = () => {
    ctx.fillStyle = 'rgba(0,0,0,0.05)'//填充背景颜色
    ctx.fillRect(0, 0, canvas.width, canvas.height)//背景
    ctx.fillStyle = "#0f0"; //文字颜色
    Arr.forEach((item, index) => {
        ctx.fillText(str[ Math.floor(Math.random() * str.length) ], index * 10, item + 10)
        Arr[index] = item >= canvas.height || item > 10000 *  Math.random() ? 0 : item + 10; //添加随机数让字符随机出现不至于那么平整
    })
    console.log(Arr);
    
}
setInterval(rain, 40)
```

### class类

1. class 的基本用法 继承 和 类型约束

```ts
class Person {
    name: string;
    age: number;

    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }

    run() {
        console.log(`${this.name} is running`);
    }

    nameInfo() {
        console.log(`My name is ${this.name}, and I am ${this.age} years old.`);
    }
}

let person = new Person('Alice', 30);
person.run();
person.nameInfo();
```

2. class 的修饰符 readonly  protected private  public

```typescript
class Person {
    public name: string; // 使用public 修饰符 可以让你定义的变量 内部访问 也可以外部访问 如果不写默认就是public
    public age: number; // 使用public 修饰符 可以让你定义的变量 内部访问 也可以外部访问 如果不写默认就是public
    private secret: string = 'This is a secret'; // 使用private 修饰符 可以让你定义的变量 只能在类的内部访问 不能被子类访问 也不能被外部访问
    protected some: any; // 使用protected 修饰符 可以让你定义的变量 内部访问 但是外部无法访问 只能被子类访问

    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }

    run() {
        console.log(`${this.name} is running`);
    }

    nameInfo() {
        console.log(`My name is ${this.name}, and I am ${this.age} years old.`);
    }
}

let person = new Person('Alice', 30);
person.run();
person.nameInfo();
```

3. super 原理

```
class A {
    name: string
    constructor(name: string) {
        this.name = name
    }

    run() {
        console.log('run')
    }
}
class Person extends A {
	 constructor(name: string, asd: string) {
        super(name);
        super.run() //调用父类的方法
    }
}
```

4. 静态方法

一、我们用static 定义的属性 不可以通过this 去访问 只能通过类名去调用

二、static 静态函数 同样也是不能通过this 去调用 也是通过类名去调用

三、需注意： 如果两个函数都是static 静态的是可以通过this互相调用

```typescript
class Person {
    public name: string; // 使用public 修饰符 可以让你定义的变量 内部访问 也可以外部访问 如果不写默认就是public
    public age: number = 10; // 使用public 修饰符 可以让你定义的变量 内部访问 也可以外部访问 如果不写默认就是public
    private secret: string = 'This is a secret'; // 使用private 修饰符 可以让你定义的变量 只能在类的内部访问 不能被子类访问 也不能被外部访问
    protected some: any; // 使用protected 修饰符 可以让你定义的变量 内部访问 但是外部无法访问 只能被子类访问

    static info: string = 'This is a static property';

    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
        // this.info //不行, 对应上面的第一点
        // this.run() //不行, 对应上面第二点
    }

    static run() {
        // console.log(`${this.name} is running`);
        return this.nameInfo();
    }

    static nameInfo() {
        return `The name is ${this.name}`;
    }
}

let person = new Person('Alice', 30);
Person.info
console.log(Person.info) //访问静态属性
Person.run();
Person.nameInfo();
```

5. get set

```typescript
interface PersonClass {
    get(type: boolean): string | number
}

interface PersonClass2 {
    set(type: boolean, value: string | number): void,
    asd: string
}

class A {
    name: string
    constructor(name: string) {
        this.name = name
    }

    run() {
        console.log('run')
    }
}

class Person extends A implements PersonClass, PersonClass2 {
    asd: string
    constructor(name: string, asd: string) {
        super(name);
        super.run() //调用父类的方法
        console.log(this.name) //张三
        this.asd = asd;
    }
    get(type: boolean): string | number {
        if (type) {
            return this.name
        } else {
            return this.asd.length
        }
    }
    set(type: boolean, value: string | number): void {
        if (type) {
            this.name = value as string
        } else {
            this.asd = value as string
        }
    }
}

const person = new Person('张三', 'asd')
console.log(person.get(true)) //张三
console.log(person.get(false)) //3
```

抽象类

**不能直接实例化**

```typescript
abstract class Animal {
    abstract makeSound(): void;
    move(): void {
        console.log("Moving...");
    }
}

// 错误！不能直接实例化抽象类
// let animal = new Animal(); // 编译错误

// 正确！通过继承来使用
class Dog extends Animal {
    makeSound(): void {
        console.log("Woof!");
    }
}
let dog = new Dog(); // 正确
```

### 元组类型

```typescript
let arr: [number, string] = [1, '2'] //元组类型 可以指定数组中每个元素的类型和位置
// arr[0] = '1' //错误 因为第一个元素必须是number类型
arr[0] = 2 //正确
// 没有设置boolean类型的元素 但是可以使用push方法添加元素 因为元组类型是一个数组类型 可以使用数组的方法
// 会导致类型不安全 因为元组类型只能访问指定位置的元素 但是push方法可以添加任意类型的元素
arr.push(true) //元组类型可以使用push方法添加元素 但是不能使用索引访问新添加的元素 因为元组类型只能访问指定位置的元素
// console.log(arr[3]) //错误 因为索引3超出范围
console.log(arr) //正确 输出 [2, '2', true, 3]
```

**应用场景 例如定义excel返回数据**

```typescript
let excel: [string, string, number, string][] = [
    ['title', 'name', 1, '123'],
    ['title', 'name', 1, '123'],
    ['title', 'name', 1, '123'],
    ['title', 'name', 1, '123'],
    ['title', 'name', 1, '123'],
]
```

### 枚举类型

#### 数字枚举

```ts
enum Typs {
    Red,
    Green,
    Blue
}
// 默认是
enum Typs {
    Red = 0,
    Green = 1,
    Blue = 2
}
// 增长枚举就是将第一个枚举的值改成1
enum Typs {
    Red = 1,
    Green,
    Blue
}
// 其他成员会从1开始自动增长
```

#### 字符串枚举

```ts
enum Typs {
    Red = 'red',
    Green = 'green',
    Blue = 'blue'
}
```

#### 异构枚举

枚举可以混合字符串和数字

```ts
enum Typs {
	NO = 'No',
	Yes = 1
}
```

#### 接口枚举

定义一个枚举Types 定义一个接口A 他有一个属性red 值为Types.yyds

声明对象的时候要遵循这个规则

```ts
enum Types {
	yyds,
    dddd
}
interface A {
    red:Types.yyds
}
 
let obj:A = {
    red:Types.yyds
}
```

#### const枚举

let  和 var 都是不允许的声明只能使用const

大多数情况下，枚举是十分有效的 方案。 然而在某些情况下需求很严格。 为了避免在额外生成的代码上的开销和额外的非直接的对枚举成员的访问，我们可以使用 const枚举。 常量枚举通过在枚举上使用 const修饰符来定义

const 声明的枚举会被编译成常量

普通声明的枚举编译完后是个对象

```ts
const enum Typs2 {
    Red = 1,
    Green = 2,
    Blue = 4
}

console.log(Typs2.Red); // Output: 1
console.log(Typs2.Green); // Output: 2
console.log(Typs2.Blue); // Output: 4
```

**反向映射**

```ts
enum Typs {
    Red,
    Green,
    Blue
}

const color: Typs = Typs.Green;
console.log(color); // Output: 1

// 反向映射
const colorName: string = Typs[color] ?? "Unknown";
console.log(colorName); // Output: "Green"
```

### 什么是类型推论

```ts
// 1.我声明了一个变量但是没有定义类型
// TypeScript 会在没有明确的指定类型的时候推测出一个类型，这就是类型推论
let str = "是的分类"

//所以TS帮我推断出来这是一个string类型
str = 12316156 //赋值不了

console.log(str)
```

```ts
// 不能够在赋值给别的类型
// 2.如果你声明变量没有定义类型也没有赋值这时候TS会推断成any类型可以进行任何操作

let str

str = 'hello world'
str = 123
str = true

console.log(str)
```

#### 类型别名

type 关键字（可以给一个类型定义一个名字）多用于复合类型

 定义类型别名

```ts
type str = string
 
 
let s:str = "啊什么的了"
console.log(s);
```

定义函数别名

```typescript
type str = () => string;

let a: str = () => "Hello, World!";

console.log(a()); // 输出: Hello, World!
```

定义联合类型别名

```ts
type str2 = string | number;
let b: str2 = "Hello";
let c: str2 = 42;
console.log(b); // 输出: Hello
console.log(c); // 输出: 42
```

定义值的别名

```ts
type value = boolean | number | string | symbol | bigint | null | undefined;

// 交叉类型
let s: value = true
let n: value = 123
let str: value = 'hello'

console.log(s, n, str)
// ----------------------------------------------------------------------------
type value = boolean | 1 | string | symbol | bigint | null | undefined;

// 交叉类型
let s: value = true
let n: value = 1
let str: value = 'hello'

console.log(s, n, str)
```

type 和 interface 还是一些区别的 虽然都可以定义类型

1.interface可以继承  type 只能通过 & 交叉类型合并

2.type 可以定义 联合类型 和 可以使用一些操作符 interface不行

3.interface 遇到重名的会合并 type 不行

type高级用法

左边的值会作为右边值的子类型遵循图中上下的包含关系

```ts
// 1 extends number ? 1 : 0  // 结果是 1
// 1 是数字字面量类型，它可以赋值给 number 类型，所以返回 1
type a = 1 extends number ? 1 : 0; // 1

// 1 extends Number ? 1 : 0  // 结果是 1  
// Number 是包装对象类型，number 类型可以赋值给 Number 类型，所以返回 1
type b = 1 extends Number ? 1 : 0; // 1

// 1 extends Object ? 1 : 0  // 结果是 1
// Object 是所有对象类型的基类，在联合类型分配时会有特殊处理
type c = 1 extends Object ? 1 : 0; // 1

// 1 extends any ? 1 : 0  // 结果是 1
// any 类型可以接受任何类型，所以返回 1
type d = 1 extends any ? 1 : 0; // 1

// 1 extends unknown ? 1 : 0  // 结果是 1
// unknown 是顶级类型，所有类型都可以赋值给它，所以返回 1
type e = 1 extends unknown ? 1 : 0; // 1
 
// 1 extends never ? 1 : 0  // 结果是 0
// never 是一个没有值的类型，任何类型都不能赋值给 never，所以返回 0
type f = 1 extends never ? 1 : 0 //0
```

### never类型

```ts
// TypeScript 将使用 never 类 型来表示不应该存在的状态(很抽象是不是)
// 返回never的函数必须存在无法达到的终点

// 因为必定抛出异常，所以 error 将不会有返回值
function error(message: string): never {
    throw new Error(message);
}
// 睡眠函数，返回一个 Promise<void>，表示在指定时间后完成
function sleep(ms: number): Promise<void> {
    return new Promise(resolve => setTimeout(resolve, ms));
}
// 因为存在死循环，所以 loop 将不会有返回值
async function loop(): Promise<never> {
    while (true) {
        console.log("This will loop forever");
        await sleep(1000);
    }
}

// 返回 never 的函数必须存在无法达到的终点
function fail() {
    return error("Something failed");
}

// console.log(fail()); // 这里会抛出异常，永远不会有返回值
// console.log(loop()); // 这里会进入死循环，永远不会有返回值
```

#### never与void的差异

```ts
//void类型只是没有返回值 但本身不会出错
function Void(): void {
    console.log('123');
}

//只会抛出异常没有返回值
function Never(): never {
    throw new Error('aaa')
}
// console.log(Void())
// console.log(Never()) //会抛出异常
```

差异2  当我们鼠标移上去的时候会发现 只有void和number  never在联合类型中会被直接移除

```ts
type A = void | number | never
```

#### never 类型的一个应用场景

```ts
type A = 'a' | 'b' | 'c';

function foo(value: A) {
    switch (value) {
        case 'a':
            console.log('Value is a');
            break;
        case 'b':
            console.log('Value is b');
            break;
        case 'c':
            console.log('Value is c');
            break;
        default:
            // 使用 never 类型来确保所有可能的情况都被处理了
            const error: never = value;
            return error;
    }
}
console.log(foo('a')); // Value is a
console.log(foo('d')); // This will cause a compile-time error
```

