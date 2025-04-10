<template>
  <div>2s</div>
  <div>1</div>
</template>

<script setup lang="ts">
// const str: string = 'hello world'
// const num: number = 123
// const bool: boolean = true
// let u: undefined = undefined;
// let n: null = null;
// console.log(str);

// let anys: any = 4;
// let unknowns: unknown = 4;

// interface User {
//   name: string;
// }
// interface person extends User{
//   age?: number;
// }
// let user: person = {
//   name: 'John'

// }
// interface User {
//   name: string;
//   [name: string]: any;
//   readonly sex: string;
//   getId: () => string;
// }
// let User: User = {
//   name: "John",
//   age: 18,
//   sex: "男",
//   getId: () => {
//     return "123";
//   },
// };
// const id = User.getId();
// console.log(id);

// let arr: Array<number> = [1, 2, 3, 4];
// let arr2: Array<string> = ["1", "2", "3", "4"];
// let arr3: Array<any> = ["1", 2, "3", null];

// interface NumberArray{
//   [index: number]: number;
// }
// let arr4: NumberArray = [1, 2, 3, 4];
// console.log(arr4[1]);
// function findNum(num: number[]): number[];

// // 重载签名2：处理string数组
// function findNum(num: string[]): string[];

// // 实现签名
// function findNum(num: any[]): any[] {
//     return num.filter(item => typeof item === 'number' || !isNaN(Number(item)));
// }
// const arr=findNum([1, "2", "3a", null, "abc"])

// function Arr(...args:any): void {
//     console.log(arguments)

//     //ts内置对象IArguments 定义
//     let arr:IArguments = arguments
// }
// console.log(arr);
// function addNum(a: number, b: number = 199): number {
//   return a + b;
// }
// const sum = addNum(1);
// console.log(sum);
// ['game','music']
// interface Person {
//   name: string;
//   aihao: string[];
//   addAihao(this: Person, aihao: string): void;
// }
// let person: Person = {
//   name: "fkk",
//   aihao: ["game", "music"],
//   addAihao(this: Person, aihao: string): void {
//     this.aihao.push(aihao)
//     console.log(person);
//   },
// };
// person.addAihao("sport");

// function fn(params:number):void//第一套规则
// function fn(params:string,params2:number):void//第二套规则
// function fn(params:any,params2?:any):void{
//   console.log(params)
//   console.log(params2)
// }
// fn(1,1)

// let myPhone: number | string = "010-820";
// myPhone = 123456789;

// let fn = function (type: number | boolean): boolean {
//   return !!type; //将type强行转化为布尔值类型，如果没用进行转化的话是会报错的
// };
// interface man {
//   sex: string;
// }
// interface person {
//   name: string;
//   age: number;
// }
// const fkk: man & person = {
//   sex: "男",
//   name: "fkk",
//   age: 18,
// };
// const getFkkFunc = (user: man & person): man & person => {
//   return user;
// };
// console.log(getFkkFunc(fkk));
// let fn = (num: string | number) => {
//   console.log((<string>num).length);
// };
// fn("123");
// let xx:object = document.querySelectorAll("div");
// console.log(typeof xx);
// class Greeter {
//     greeting: string;
//     constructor(message: string) {
//         this.greeting = message;
//     }
//     greet() {
//         return "Hello, " + this.greeting;
//     }
// }

// let greeter = new Greeter("world");
// console.log(greeter.greet());
class Point {
  x;
  y;
  constructor(x:number, y:number) {
    this.x = x;
    this.y = y;
  }

  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }
}

let point = new Point(2, 3);
console.log(point.x,point.y);
class Foo {
  static bar() {
    this.baz();
  }
  static baz() {
    console.log('hello');
  }
  baz() {
    console.log('world');
  }
}

// Foo.bar() // hell
const foo1=new Foo();
foo1.baz();
</script>

<style>
</style>