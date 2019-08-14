---
title: TS手册指南
date: 2019-07-05 11:54:59
tags: [typescript]
cover_img:
feature_img:
description:
keywords: TS | typescript
---
### 基础类型

#### 布尔值
```
let isNone: boolean = false;
```

#### 数字
```
let decLiteral: number = 6;
```

#### 字符串
```
let name: string = `YC`
```

#### 数组
```
let list: number[] = [1, 2, 3];
```

#### 元组
```
let x: [string, number];
// OK
x = ['hello', 10];
// Error
x = [10, 'hello'];
```

#### 枚举
```
enum Color {Red = 1, Green, Blue}
let colorName: string = Color[2];

console.log(colorName);  // 显示'Green'因为上面代码里它的值是2
```

#### Any（不清楚变量类型，不希望类型检查器对这些值进行检查）
```
let notSure: any = 4;
notSure = "maybe a string instead";
notSure = false; // okay, definitely a boolean
```

#### Void(void类型与any类型相反，它表示没有任何类型。)
```
function warnUser(): void {
    console.log("This is my warning message");
}
声明一个void类型的变量没有什么大用，因为你只能为它赋予undefined和null
```

#### Null和Undefined
```
// Not much else we can assign to these variables!
let u: undefined = undefined;
let n: null = null;
```

#### Never
never类型表示的是那些永不存在的值的类型。 例如， never类型是那些总是会抛出异常或根本就不会有返回值的函数表达式或箭头函数表达式的返回值类型； 变量也可能是 never类型，当它们被永不为真的类型保护所约束时。
```
// 返回never的函数必须存在无法达到的终点
function error(message: string): never {
    throw new Error(message);
}

// 推断的返回值类型为never
function fail() {
    return error("Something failed");
}

// 返回never的函数必须存在无法达到的终点
function infiniteLoop(): never {
    while (true) {
    }
}
```

#### Object
object表示非原始类型，也就是除number，string，boolean，symbol，null或undefined之外的类型。
```
declare function create(o: object | null): void;

create({ prop: 0 }); // OK
create(null); // OK
```

#### 类型断言
你比机器更清楚自己干什么。
```
// “尖括号”语法：
let someValue: any = "this is a string";

let strLength: number = (<string>someValue).length;

// as 语法：
let someValue: any = "this is a string";

let strLength: number = (someValue as string).length;
```

### 接口
接口可以理解为入参规范
```
// 带有问号为可选属性
interface SquareConfig {
  color?: string;
  width?: number;
}

function createSquare(config: SquareConfig): {color: string; area: number} {
  let newSquare = {color: "white", area: 100};
  if (config.color) {
    newSquare.color = config.color;
  }
  if (config.width) {
    newSquare.area = config.width * config.width;
  }
  return newSquare;
}

let mySquare = createSquare({color: "black"});
```

#### 只读属性
一些对象属性只能在对象刚刚创建的时候修改其值。
```
interface Point {
    readonly x: number;
    readonly y: number;
}
let p1: Point = { x: 10, y: 20 };
p1.x = 5; // error!
```

#### 函数类型
定义一个函数的入参和返回值
```
interface SearchFunc {
  (source: string, subString: string): boolean;
}
let mySearch: SearchFunc;
mySearch = function(source: string, subString: string) {
  let result = source.search(subString);
  return result > -1;
}
```

#### 定义class类型接口
```
interface ClockInterface {
    currentTime: Date;
    setTime(d: Date);
}

class Clock implements ClockInterface {
    currentTime: Date;
    setTime(d: Date) {
        this.currentTime = d;
    }
    constructor(h: number, m: number) { }
}
```

#### 继承接口
```
interface Shape {
    color: string;
}

interface PenStroke {
    penWidth: number;
}

interface Square extends Shape, PenStroke {
    sideLength: number;
}

let square = <Square>{};
square.color = "blue";
square.sideLength = 10;
square.penWidth = 5.0;
```
