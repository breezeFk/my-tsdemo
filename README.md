# TypeScript学习
TS是JS的超集
## 数据类型
### 基础类型

- Boolean
- Number
- String
- null
- undefined
- Symbol(es6)
- BigInt(es10)

```typescript
let str: string = 'hello world'
let num: number = 123
let bool: boolean = true
let u: undefined = undefined;
let n: null = null;
```



### 空值类型

JavaScript 没有空值（Void）的概念，在 [TypeScript](https://so.csdn.net/so/search?q=TypeScript&spm=1001.2101.3001.7020) 中，可以用 `void` 表示没有任何返回值的函数

```typescript
function voidFn(): void {
    console.log('test void')
}
//void也可以定义undefined 和 null类型
let u: void = undefined
let n: void = null;
```
### 任意类型
1. 没有强制限定哪种类型，随时切换类型都可以 我们可以对 any 进行任何操作，不需要检查类型
2. 声明变量的时候没有指定任意类型默认为any
3. 弊端:如果使用any 就失去了TS类型检测的作用
4. TypeScript 3.0中引入的 unknown 类型也被认为是 top type ，但它更安全。与 any 一样，所有类型都可以分配给unknown

```typescript
let anys: any = 4;
let unknowns: unknown = 4;
```
#### 区别
1. unknown类型不能赋值给其他类型,不能作为子类型只能作为父类型 any可以作为父类型和子类型
2. unknow 不能调用属性和方法
```typescript
// 错误: 不能将unknown赋值给其他类型
let names:unknown = '123'
let names2:string = names

// 正确: any可以作为子类型
let names:any = '123'
let names2:string = names

//unknown可赋值对象只有unknown 和 any
let bbb:unknown = '123'
let aaa:any= '456'
aaa = bbb

// 如果是any类型在对象没有这个属性的时候还在获取是不会报错的
let obj:any = {b:1}
obj.a
 
 
// 如果是unknow 是不能调用属性和方法
let obj:unknown = {b:1,ccc:():number=>213}
obj.b
obj.ccc()
```
### 数组类型

数组的类型

```typescript
//类型加中括号
let arr1: number[] = [1, 2, 3]; //数字类型的数组
let arr2: string[] = ["1", "2"]; //字符串类型的数组
let arr3: any[] = [1, "2", true]; //任意类型的数组

//规则 Array<类型>
let arr: Array<number> = [1, 2, 3, 4];
let arr2: Array<string> = ["1", "2", "3", "4"];
let arr3: Array<any> = ["1", 2, "3", null];
```

#### 用接口表示数组

```typescript
interface NumberArray{
  [index: number]: number;
}
let arr4: NumberArray = [1, 2, 3, 4];
console.log(arr4[1]);
```

### 多维数组

```typescript
let data:number[][] = [[1,2], [3,4]];
```

### arguments类数组

arguments 是一个类数组对象（array-like object），它包含了函数被调用时传入的所有参数
```typescript
function Arr(...args:any): void {
    console.log(arguments) 
    
    //ts内置对象IArguments 定义
    let arr:IArguments = arguments
}
Arr(111, 222, 333)

//其中 IArguments 是 TypeScript 中定义好了的类型，它实际上就是：
interface IArguments {
[index: number]: any;
length: number;
callee: Function;
}
```

### 联合类型|类型断言|交叉类型

#### 联合类型
```typescript
let myPhone: number | string = '010-820';
myPhone = 123456789;
```
#### 函数使用联合类型
应用场景，比如后端返回一个数字0或者1，但实际上需要是布尔值，就可以使用联合类型
```typescript
let fn = function(type:number|boolean):boolean {
return !!type//将type强行转化为布尔值类型，如果没用进行转化的话是会报错的
}
```
#### 交叉类型
多种类型的集合，联合对象将具有所联合类型的所有成员
```typescript
interface man {
  sex: string;
}
interface person {
  name: string;
  age: number;
}
const fkk: man & person = {
  sex: "男",
  name: "fkk",
  age: 18,
};
const getFkkFunc = (user: man & person): man & person => {
  return user;
};
console.log(getFkkFunc(fkk));
```
#### 类型断言
语法格式，值 as 类型 或者 <类型>值
需要注意的是，类型断言只能够「欺骗」TypeScript 编译器，无法避免运行时的错误，反而滥用
类型断言可能会导致运行时错误
覆盖它的推断，并且能以你任何你想要的方式分析它，这种机制被称为「类型断言」。TypeScript
类型断言用来告诉编译器你比它更了解这个类型，并且它不应该再发出错误
当 S 类型是 T 类型的子集，或者 T 类型是 S 类型的子集时， S 能被成功断言成 T 。这是为了
在进行类型断言时提供额外的安全性，完全毫无根据的断言是危险的，如果你想这么做，你可以使
用 any 。
2、类型断言的用途
（1）将一个联合类型推断为其中一个类型
（2）将一个父类断言为更加具体的子类
（3）将任何一个类型断言为 any
（4）将 any 断言为一个具体的类型 
```typescript
// 原型：
let fn = function(num:number | string):void{
    console.log(num.length);//这里会报错，因为我们确实没有.length这个内容
}
fn("12345")
--------------------------------------------------------
// 断言写法
let fn = function(num:number | string):void{
    // console.log((<string>num).length);
    console.log((num as string).length);//用括号括起来，as断言他是string类型
}
fn("12345")//这样会打印出5
fn(12345)//这样会打印出undefined
```
## interface

在typescript中，我们定义对象的方式要用关键字interface（接口）,使用interface来定义一种约束，让数据的结构满足约束的格式。
1. 接口约束的时候不能多一个属性也不能少一个属性,必须与接口保持一致
2. 接口可以重名、合并
```typescript
// interface Person {
//     name: string;
//     age: number;
// }
// 可以重名、合并
interface Person {
  name: string;
}
interface Person {
  age: number;
}
let person: Person = {
    name: 'fkk',
    age: 18
}
```
### extends 继承
```typescript
interface User {
  name: string;
}
interface person extends User{
  age: number;
}
let user: person = {
  name: 'fkk',
  age: 25
}
```
### 可选属性 使用?操作符
可选属性的含义是该属性可以不存在
```typescript
interface Person {
    name: string;
    age?: number;
}
let person: Person = {
    name: 'fkk'
}
```
### 任意属性 [propName: string]
```typescript
interface User {
  name: string;
  [propName: string]: any;
}
let User: User = {
  name: 'John',
  age: 18,
  sex: '男'
}
```
### 只读属性 readonly
readonly 只读属性是不允许被重新赋值的只能读取
```typescript
interface User {
  name: string;
  [name: string]: any;
  readonly sex: string;
}
let User: User = {
  name: "John",
  age: 18,
  sex: "男",
};
User.sex = "女"; // 报错
```
### 添加函数
```typescript
interface User {
  name: string;
  [name: string]: any;
  readonly sex: string;
  getId:()=>string
}
let User: User = {
  name: "John",
  age: 18,
  sex: "男",
  getId:()=>{
    return '123'
  }
};
const id=User.getId()
console.log(id);
```

### 内置对象

JavaScript 中有很多[内置对象](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects)，它们可以直接在 [TypeScript](https://so.csdn.net/so/search?q=TypeScript&spm=1001.2101.3001.7020) 中当做定义好了的类型。

#### ECMAScript 的内置对象

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

#### DOM 和 BOM 的内置对象

```typescript
let body: HTMLElement = document.body;
let allDiv: NodeList = document.querySelectorAll('div');
//读取div 这种需要类型断言 或者加个判断应为读不到返回null
let div:HTMLElement = document.querySelector('div') as HTMLDivElement
```

#### 定义Promise

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

## 类

## 类型操作

### 函数扩展

#### 函数的类型与返回值

函数的类型

```typescript
function addNum(a:number,b:number):number{
    return a+b
}
const sum = addNum(1,2)
console.log(sum); //3
```

#### 函数的可选参数? 和 默认值
```typescript
function addNum(a:number,b?:number):number{
    return a+b
}
const sum = addNum(1)
console.log(sum); //NaN 因  为b没有传值为undefined
```
```typescript
function addNum(a:number,b:number=199):number{
    return a+b
}
const sum = addNum(1)
console.log(sum); //200 因为b没有传值.默认为199，可选参数和默认值不能同时存在
```


#### 定义接口函数
```typescript
interface Person {
  name: string;
  aihao: string[];
  addAihao(this: Person, aihao: string): void;
}
let person: Person = {
  name: "fkk",
  aihao: ["game", "music"],
  addAihao(this: Person, aihao: string): void {
    this.aihao.push(aihao)
    console.log(person);
  },
};
person.addAihao("sport");
```
#### 函数重载

- 重载是方法名字相同，而参数不同，返回类型可以相同也可以不同。
- 如果参数类型不同，则参数类型应设置为 any。 
- 参数数量不同你可以将不同的参数设置为可选。

为了让编译器能够选择正确的检查类型，它与 JavaScript 里的处理流程相似。 它查找重载列表， 尝试使用第一个重载定义。 如果匹配的话就使用这个。 因此，在定义重载的时候，一定要把最精 确的定义放在最前面。

```typescript
function fn(params:number):void//第一套规则
function fn(params:string,params2:number):void//第二套规则
function fn(params:any,params2?:any):void{
	console.log(params)
	console.log(params2)
}
let a = fn(1,1)
//输出1跟1，因为遵循的是第三套规则
let a = fn("1",1)
//输出"1"跟1，遵循的是第二套规则
```



## tsconfig.json

## tsc