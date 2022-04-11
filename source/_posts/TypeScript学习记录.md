title: TypeScript学习记录
author: 黄罐头
tags: ['typescript']
categories: web

date: 2022-3-27 15:06:00
---
## 基础类型

### 数字 number

```typescript
const level: number = 6
```

### 字符串 string

```typescript
cosnt name: string: "huangping"
```

### 布尔值 boolean

```typescript
const isBoy: boolean = true
```

### 数组 array

```typescript
const list: number[] = [1, 2, 3]
```

### 元组 Tuple

```typescript
let x: [string, number];
x = ['hello', 10]
```

### 枚举 enum

```typescript
enum Color { Red, Green, Yellow }
let c: Color = Color.Green;
```

### 任意值 any

```typescript
let a: any = 4
a = 'huangping'
```

### 空值 void

```typescript
function voidFunc(): void {
	console.log('void')
}
```

### Null和Undefined

### Never

### 类型断言

```typescript
let someValue: any = "this is a string";
let strLength: number = (<string>someValue).length;
or
let strLength: number = (someValue as string).length;
```

## 接口

用interface关键字定义一个接口

* 当接属性可选时，可在属性名字定义后面加上一个`?`符号
* 只读属性，可在属性名前用readonly来指定

```typescript
interface person {
	name: string;
    age: number;
    address?: string;
    readonly sex: string;
}
```

