## Javascript学习

**数组遍历方法**

```js
const arr = [110,120,130]
```

`map()` 方法会遍历数组中的每个元素

- 涉及：`map()` 方法的用法和返回值
- 箭头函数的隐式返回规则

```js
arr.map(i => {
    return i
})
```

**数组对象操作**

遍历输出而不需要返回新数组，使用 `forEach` 只遍历执行，不返回任何值（总是 `undefined`）

- 涉及：对象数组的遍历
- `map()` 方法的实际应用
- 如何访问数组中的对象元素

```js
const obj = [{'name':'小明'，age:10},{'name':'小李'，age:11}];
```

```js
obj.map(i => { return i })
```

```js
obj.forEach(i => {
    console.log(i)
})
```

两个数组合并，根据 `name` 进行匹配，生成包含完整信息的新数组。

**使用 `map` 和 `find`**

```js
const merged = obj.map(i =>{
    const matched = objSex.find(sexItem => sexItem.name === i.name);
    return {
        ...i,
        ...matched
    }
})

console.log(merged)
```

| 特性               |    `forEach`     |  `map`   |
| :----------------- | :--------------: | :------: |
| **返回值**         |   `undefined`    |  新数组  |
| **用途**           |     执行操作     | 转换数据 |
| **是否改变原数组** | 通常不（但可以） |  不改变  |
| **链式调用**       |      不可以      |   可以   |

**对象（Object）中的键值**

```js
// 对象就是键值对的集合
const person = {
    name: '小明',    // 键: 'name', 值: '小明'
    age: 18,        // 键: 'age', 值: 18
    city: '北京'     // 键: 'city', 值: '北京'
};
```

**Map 中的键值对**

```js
// Map 也是键值对的集合
const personMap = new Map();
personMap.set('name', '小明');  // 键: 'name', 值: '小明'
personMap.set('age', 18);      // 键: 'age', 值: 18
personMap.set('city', '北京');  // 键: 'city', 值: '北京'
```

**数组对象中的键值对**

```js
// 数组中的每个元素都是包含键值对的对象
const users = [
    {name: '小明', age: 18, city: '北京'},  // 第一个对象的键值对
    {name: '小李', age: 20, city: '上海'}   // 第二个对象的键值对
];
```

**操作键值对的方法**

```js
const person = {name: '小明', age: 18};

// 点表示法
console.log(person.name); // '小明'

// 方括号表示法
console.log(person['age']); // 18
```

**遍历键值对**

```js
const person = {name: '小明', age: 18, city: '北京'};

//遍历键
Object.keys(person).forEach(k => {
    console.log(k)
})

//遍历值
Object.values(person).forEach(V => {
    console.log(V)
})

//遍历键值对
Object.entries(person).forEach(([k,v]) => {
    console.log(`${k}: ${v}`);
})
```

**合并对象**

```js
const obj1 = {name: '小明', age: 18};
const obj2 = {name: '小明', city: '北京', gender: '男'};

// 合并键值对
const merged = {...obj1, ...obj2};
console.log(merged);
```

 **数组方法中的键值对操作**

```js
const users = [
    {name: '小明', age: 18},
    {name: '小李', age: 20}
];

// 提取特定键的值
const names = users.map(user => user.name);
console.log(names); // ['小明', '小李']

// 过滤基于键值对
const adults = users.filter(user => user.age >= 18);
console.log(adults); // 两个对象都会保留

// 转换为新的键值对结构
const userMap = users.reduce((map, user) => {
    map[user.name] = user.age;
    return map;
});
console.log(userMap); // {小明: 18, 小李: 20}
```

## 响应式打开组件的方法

```html
<el-button @click="OpenDetails(scope.row)" type="text" size="small">详情</el-button>
<el-button @click="OpenRating(scope.row)" type="text" size="small">评级</el-button>

// 这里是组件
<Details v-model="isDetailsOpen" :row="selectedRow"></Details>
<Rating @success="getTableData" v-model="isRatingOpen" :row="selectedRow"></Rating>

// 赋值
data() {
	return {
		selectedRow: {},
		isDetailsOpen: false,
		isResignOpen: false,
	}
}

// 打开的方法
OpenDetails(row) {
			this.selectedRow = row
			this.isDetailsOpen = true
		},

OpenResign(row) {
			this.selectedRow = row
			this.isResignOpen = true
		},

// 组件内容
<template>
	<div>
		<el-drawer title="个人详情" :visible.sync="drawer" :before-close="handleClose" append-to-body size="100%">
			<FormDetails :tableData="tableData"></FormDetails>
		</el-drawer>
	</div>
</template>

<script>
import FormDetails from './FormDetails'
export default {
	model: {
		prop: 'state',
		event: 'change'
	},
	props: {
		state: {
			type: Boolean,
			default: false
		},
		row: {
			type: Object,
			default: () => ({})
		}
	},
	data() {
		return {
			drawer: false,
		}
	},
	watch: {
		state: {
			immediate: true,
			handler(val) {
				this.drawer = val
				if (val) {
					this.getTableData()
				}
			}
		},
		drawer: {
			handler(val) {
				this.$emit('change', val)
			}
		}
	}
}
</script>

<template>
	<div>
		<el-dialog title="离职" :visible.sync="dialog" width="30%" :before-close="handleClose" append-to-body>
			<el-form :model="item" label-width="60px" class="flex-center">
				<el-form-item label="备注" class="w100p">
					<el-input type="textarea" v-model="item.remark" class="w100p" />
				</el-form-item>
			</el-form>
			<span slot="footer" class="flex-center">
				<el-button @click="close()">取 消</el-button>
				<el-button type="primary" @click="submit()">确 定</el-button>
			</span>
		</el-dialog>
	</div>
</template>

<script>
export default {
	model: {
		prop: 'state',
		event: 'change'
	},
	props: {
		state: {
			type: Boolean,
			default: false
		},
		row: {
			type: Object,
			default: () => ({})
		}
	},
	data() {
		return {
			dialog: false,
			item: {
				remark: ''
			}
		}
	},
	watch: {
		state: {
			immediate: true,
			handler(val) {
				this.dialog = val
				if (val) {
					this.init()
				}
			}
		},
		dialog: {
			handler(val) {
				this.$emit('change', val)
			}
		}
	}
}
</script>
```

## fetch请求

```js
async es() {
			try {
                // 请求地址, 请求方法
				const response = await fetch('http://127.0.0.1:57598/ReaderTool/CPU_ReadCardNumber', { method: 'GET' })
				if (!response.ok) {
					throw new Error(`HTTP ${response.status}:${response.statusText}`)
				}
				const result = await response.json()
				
                console.log('完整响应:', result)
                
				this.IdCard = result.data
                
			} catch (error) {
				this.$message.error('请检查设备是否接入,程序是否启动')
			}
		}
```

