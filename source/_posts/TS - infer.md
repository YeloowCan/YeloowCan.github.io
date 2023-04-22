title: TS-infer关键字
author: 黄罐头
tags: ['typescript']
categories: web

date: 2023-04-13 22:30:58
---

## infer

在条件类型中申明泛型，使用infer关键字

有以下两个限制：

1. 只能在条件类型的extends子句中使用
2. infer得到的类型只能在true语句中使用



申明一个条件类型Element，获取数组中元素的类型：

```typescript
type ElementType<T> = T extends unknown[] ? T[number] : T
type A = ElementType<number[]> // number
```

使用infer关键字重写：

```typescript
type ElementType2<T> = T extends (infer U)[] ? U : T
type B = ElementType2<number[]> // number
```



### replace

```typescript
type Replace<
  S extends string,
  From extends string,
  To extends string
> = From extends ''
  ? S
  : S extends `${infer A}${From}${infer B}`
  ? `${A}${To}${B}`
  : S;

```



### pop

```typescript
type Pop<T extends any[]> = T extends [...infer I, infer _] ? I : [];
```

